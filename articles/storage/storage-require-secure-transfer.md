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
# <a name="require-secure-transfer"></a><span data-ttu-id="dfafa-103">Veilige overdracht vereisen</span><span class="sxs-lookup"><span data-stu-id="dfafa-103">Require secure transfer</span></span>

<span data-ttu-id="dfafa-104">De optie "Veilig vereiste gegevensoverdracht" verhoogt de beveiliging van uw storage-account door alleen aanvragen naar de storage-account van beveiligde verbindingen.</span><span class="sxs-lookup"><span data-stu-id="dfafa-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="dfafa-105">Bijvoorbeeld bij het aanroepen van REST-API's voor toegang tot uw storage-account, moet u verbinden via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dfafa-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="dfafa-106">Alle aanvragen met HTTP zijn afgewezen als "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dfafa-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="dfafa-107">Wanneer u de service Azure-bestanden gebruikt, wordt er een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dfafa-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="dfafa-108">Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van de Linux SMB-client.</span><span class="sxs-lookup"><span data-stu-id="dfafa-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="dfafa-109">De optie "Veilig vereiste gegevensoverdracht" is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dfafa-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="dfafa-110">Omdat Azure Storage biedt geen ondersteuning voor HTTPS voor aangepaste domeinnamen, is deze optie niet toegepast wanneer u een aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="dfafa-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="dfafa-111">"Veilig vereiste gegevensoverdracht" inschakelen in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="dfafa-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="dfafa-112">Kunt u de 'beveiligde overdracht vereist' beide instellen bij het maken van een opslagaccount in de [Azure-portal](https://portal.azure.com), en voor bestaande opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="dfafa-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="dfafa-113">Veilige overdracht vereisen wanneer u een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="dfafa-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="dfafa-114">Open de **storage-account maken** blade in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dfafa-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="dfafa-115">Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="dfafa-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="dfafa-117">Veilige overdracht voor een bestaand opslagaccount vereisen</span><span class="sxs-lookup"><span data-stu-id="dfafa-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="dfafa-118">Selecteer een bestaand opslagaccount in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dfafa-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="dfafa-119">Selecteer **configuratie** onder **instellingen** in de blade opslagaccount menu.</span><span class="sxs-lookup"><span data-stu-id="dfafa-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="dfafa-120">Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="dfafa-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="dfafa-122">"Veilig vereiste gegevensoverdracht" inschakelen via een programma</span><span class="sxs-lookup"><span data-stu-id="dfafa-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="dfafa-123">De naam van de instelling is _supportsHttpsTrafficOnly_ in eigenschappen van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="dfafa-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="dfafa-124">U kunt "veilige overdracht vereist' instellen met de REST-API, hulpprogramma's of bibliotheken inschakelen:</span><span class="sxs-lookup"><span data-stu-id="dfafa-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="dfafa-125">**REST-API** (versie: 2016-12-01): [releasepakket](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="dfafa-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="dfafa-126">**PowerShell** (versie: 4.1.0): [releasepakket](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="dfafa-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="dfafa-127">**CLI** (versie: 2.0.11): [releasepakket](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="dfafa-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="dfafa-128">**NodeJS** (versie: 1.1.0): [releasepakket](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="dfafa-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="dfafa-129">**.NET SDK** (versie: 6.3.0): [releasepakket](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="dfafa-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="dfafa-130">**Python SDK** (versie: 1.1.0): [releasepakket](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="dfafa-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="dfafa-131">**Ruby SDK** (versie: 0.11.0): [releasepakket](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="dfafa-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="dfafa-132">'Veilige overdracht vereist' instellen met de REST-API inschakelen</span><span class="sxs-lookup"><span data-stu-id="dfafa-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="dfafa-133">U kunt gebruiken om te vereenvoudigen testen met de REST-API, [ArmClient](https://github.com/projectkudu/ARMClient) aan te roepen vanuit de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="dfafa-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="dfafa-134">U kunt hieronder vanaf de opdrachtregel gebruiken om te controleren van de instelling met de REST-API:</span><span class="sxs-lookup"><span data-stu-id="dfafa-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="dfafa-135">U kunt vinden in het antwoord _supportsHttpsTrafficOnly_ instelling.</span><span class="sxs-lookup"><span data-stu-id="dfafa-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="dfafa-136">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dfafa-136">Sample:</span></span>

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

<span data-ttu-id="dfafa-137">U kunt hieronder vanaf de opdrachtregel gebruiken om de instelling met de REST-API:</span><span class="sxs-lookup"><span data-stu-id="dfafa-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="dfafa-138">Voorbeeld van Input.json:</span><span class="sxs-lookup"><span data-stu-id="dfafa-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="dfafa-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfafa-139">Next steps</span></span>
<span data-ttu-id="dfafa-140">Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen kunnen ontwikkelaars om beveiligde toepassingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="dfafa-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="dfafa-141">Voor meer informatie gaat u naar de [opslag beveiligingshandleiding](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="dfafa-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
