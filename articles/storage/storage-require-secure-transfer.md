---
title: aaaRequire veilige overdracht in Azure Storage | Microsoft Docs
description: Meer informatie over 'Vereisen veilige overdracht' Hallo-functie voor Azure Storage en hoe tooenable deze.
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Veilige overdracht vereisen

Hallo 'beveiligde transfer-vereist' optie verhoogt Hallo beveiliging van uw storage-account door alleen aanvragen toohello storage-account van beveiligde verbindingen. Bijvoorbeeld bij het aanroepen van REST-API's tooaccess uw storage-account, moet u verbinden via HTTPS. Alle aanvragen met HTTP zijn afgewezen als "Veilig vereiste gegevensoverdracht" is ingeschakeld.

Wanneer u hello Azure Files service gebruikt, wordt een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld. Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van het Hallo Linux SMB-client. 

Hallo 'beveiligde transfer-vereist' optie is standaard uitgeschakeld.

> [!NOTE]
> Omdat Azure Storage biedt geen ondersteuning voor HTTPS voor aangepaste domeinnamen, is deze optie niet toegepast wanneer u een aangepaste domeinnaam.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Inschakelen van 'Veilige overdracht vereist' in hello Azure-portal

U kunt inschakelen Hallo 'veilige overdracht vereist' beide instellen wanneer u een opslagaccount in Hallo maken [Azure-portal](https://portal.azure.com), en voor bestaande opslagaccounts.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Veilige overdracht vereisen wanneer u een opslagaccount maken

1. Open Hallo **storage-account maken** blade in hello Azure-portal.
1. Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Veilige overdracht voor een bestaand opslagaccount vereisen

1. Selecteer een bestaand opslagaccount in hello Azure-portal.
1. Selecteer **configuratie** onder **instellingen** in de blade Hallo opslagaccount menu.
1. Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>"Veilig vereiste gegevensoverdracht" inschakelen via een programma

de naam van de instelling Hallo is _supportsHttpsTrafficOnly_ in eigenschappen van het opslagaccount. U kunt "veilige overdracht vereist' instellen met de REST-API, hulpprogramma's of bibliotheken inschakelen:

* **REST-API** (versie: 2016-12-01): [releasepakket](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (versie: 4.1.0): [releasepakket](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (versie: 2.0.11): [releasepakket](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (versie: 1.1.0): [releasepakket](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK** (versie: 6.3.0): [releasepakket](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (versie: 1.1.0): [releasepakket](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK** (versie: 0.11.0): [releasepakket](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>'Veilige overdracht vereist' instellen met de REST-API inschakelen

toosimplify testen met REST API, kunt u [ArmClient](https://github.com/projectkudu/ARMClient) toocall uit vanaf de opdrachtregel.

 U kunt gebruiken dan opdrachtregel toocheck Hallo instelling Hello REST-API:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

In het antwoord van Hallo vindt u _supportsHttpsTrafficOnly_ instelling. Voorbeeld:

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

U kunt gebruiken dan opdrachtregel tooenable Hallo instelling Hello REST-API:

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
Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen. Voor meer informatie gaat u naar Hallo [opslag beveiligingshandleiding](storage-security-guide.md).
