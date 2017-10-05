---
title: Veilige overdracht in Azure Storage vereisen | Microsoft Docs
description: Meer informatie over de functie 'Veilige overdracht vereist' voor Azure Storage en hoe deze in te schakelen.
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a>Veilige overdracht vereisen

De optie "Veilig vereiste gegevensoverdracht" verhoogt de beveiliging van uw storage-account door alleen aanvragen naar de storage-account van beveiligde verbindingen. Bijvoorbeeld bij het aanroepen van REST-API's voor toegang tot uw storage-account, moet u verbinden via HTTPS. Alle aanvragen met HTTP zijn afgewezen als "Veilig vereiste gegevensoverdracht" is ingeschakeld.

Wanneer u de service Azure-bestanden gebruikt, wordt er een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld. Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van de Linux SMB-client. 

De optie "Veilig vereiste gegevensoverdracht" is standaard uitgeschakeld.

> [!NOTE]
> Omdat Azure Storage biedt geen ondersteuning voor HTTPS voor aangepaste domeinnamen, is deze optie niet toegepast wanneer u een aangepaste domeinnaam.

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a>"Veilig vereiste gegevensoverdracht" inschakelen in de Azure portal

Kunt u de 'beveiligde overdracht vereist' beide instellen bij het maken van een opslagaccount in de [Azure-portal](https://portal.azure.com), en voor bestaande opslagaccounts.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Veilige overdracht vereisen wanneer u een opslagaccount maken

1. Open de **storage-account maken** blade in de Azure portal.
1. Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Veilige overdracht voor een bestaand opslagaccount vereisen

1. Selecteer een bestaand opslagaccount in de Azure-portal.
1. Selecteer **configuratie** onder **instellingen** in de blade opslagaccount menu.
1. Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>"Veilig vereiste gegevensoverdracht" inschakelen via een programma

De naam van de instelling is _supportsHttpsTrafficOnly_ in eigenschappen van het opslagaccount. U kunt "veilige overdracht vereist' instellen met de REST-API, hulpprogramma's of bibliotheken inschakelen:

* **REST-API** (versie: 2016-12-01): [releasepakket](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (versie: 4.1.0): [releasepakket](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (versie: 2.0.11): [releasepakket](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (versie: 1.1.0): [releasepakket](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK** (versie: 6.3.0): [releasepakket](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (versie: 1.1.0): [releasepakket](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK** (versie: 0.11.0): [releasepakket](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>'Veilige overdracht vereist' instellen met de REST-API inschakelen

U kunt gebruiken om te vereenvoudigen testen met de REST-API, [ArmClient](https://github.com/projectkudu/ARMClient) aan te roepen vanuit de opdrachtregel.

 U kunt hieronder vanaf de opdrachtregel gebruiken om te controleren van de instelling met de REST-API:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

U kunt vinden in het antwoord _supportsHttpsTrafficOnly_ instelling. Voorbeeld:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

U kunt hieronder vanaf de opdrachtregel gebruiken om de instelling met de REST-API:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Voorbeeld van Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Volgende stappen
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen kunnen ontwikkelaars om beveiligde toepassingen te bouwen. Voor meer informatie gaat u naar de [opslag beveiligingshandleiding](storage-security-guide.md).
