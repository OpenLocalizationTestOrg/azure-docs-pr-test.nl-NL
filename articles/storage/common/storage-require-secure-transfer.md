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
# <a name="require-secure-transfer"></a><span data-ttu-id="6fa7f-103">Veilige overdracht vereisen</span><span class="sxs-lookup"><span data-stu-id="6fa7f-103">Require secure transfer</span></span>

<span data-ttu-id="6fa7f-104">Hallo 'beveiligde transfer-vereist' optie verhoogt Hallo beveiliging van uw storage-account door alleen aanvragen toohello storage-account van beveiligde verbindingen.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="6fa7f-105">Bijvoorbeeld bij het aanroepen van REST-API's tooaccess uw storage-account, moet u verbinden via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="6fa7f-106">Alle aanvragen met HTTP zijn afgewezen als "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="6fa7f-107">Wanneer u hello Azure Files service gebruikt, wordt een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="6fa7f-108">Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van het Hallo Linux SMB-client.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="6fa7f-109">Hallo 'beveiligde transfer-vereist' optie is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="6fa7f-110">Omdat Azure Storage biedt geen ondersteuning voor HTTPS voor aangepaste domeinnamen, is deze optie niet toegepast wanneer u een aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="6fa7f-111">Inschakelen van 'Veilige overdracht vereist' in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6fa7f-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="6fa7f-112">U kunt inschakelen Hallo 'veilige overdracht vereist' beide instellen wanneer u een opslagaccount in Hallo maken [Azure-portal](https://portal.azure.com), en voor bestaande opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="6fa7f-113">Veilige overdracht vereisen wanneer u een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="6fa7f-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="6fa7f-114">Open Hallo **storage-account maken** blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="6fa7f-115">Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="6fa7f-117">Veilige overdracht voor een bestaand opslagaccount vereisen</span><span class="sxs-lookup"><span data-stu-id="6fa7f-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="6fa7f-118">Selecteer een bestaand opslagaccount in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="6fa7f-119">Selecteer **configuratie** onder **instellingen** in de blade Hallo opslagaccount menu.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="6fa7f-120">Onder **vereiste gegevensoverdracht Secure**, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![schermopname](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="6fa7f-122">"Veilig vereiste gegevensoverdracht" inschakelen via een programma</span><span class="sxs-lookup"><span data-stu-id="6fa7f-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="6fa7f-123">de naam van de instelling Hallo is _supportsHttpsTrafficOnly_ in eigenschappen van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="6fa7f-124">U kunt "veilige overdracht vereist' instellen met de REST-API, hulpprogramma's of bibliotheken inschakelen:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="6fa7f-125">**REST-API** (versie: 2016-12-01): [releasepakket](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="6fa7f-126">**PowerShell** (versie: 4.1.0): [releasepakket](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="6fa7f-127">**CLI** (versie: 2.0.11): [releasepakket](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="6fa7f-128">**NodeJS** (versie: 1.1.0): [releasepakket](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="6fa7f-129">**.NET SDK** (versie: 6.3.0): [releasepakket](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="6fa7f-130">**Python SDK** (versie: 1.1.0): [releasepakket](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="6fa7f-131">**Ruby SDK** (versie: 0.11.0): [releasepakket](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="6fa7f-132">'Veilige overdracht vereist' instellen met de REST-API inschakelen</span><span class="sxs-lookup"><span data-stu-id="6fa7f-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="6fa7f-133">toosimplify testen met REST API, kunt u [ArmClient](https://github.com/projectkudu/ARMClient) toocall uit vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="6fa7f-134">U kunt gebruiken dan opdrachtregel toocheck Hallo instelling Hello REST-API:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="6fa7f-135">In het antwoord van Hallo vindt u _supportsHttpsTrafficOnly_ instelling.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="6fa7f-136">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-136">Sample:</span></span>

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

<span data-ttu-id="6fa7f-137">U kunt gebruiken dan opdrachtregel tooenable Hallo instelling Hello REST-API:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="6fa7f-138">Voorbeeld van Input.json:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="6fa7f-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6fa7f-139">Next steps</span></span>
<span data-ttu-id="6fa7f-140">Azure Storage biedt een uitgebreide reeks beveiligingsmogelijkheden die samen ontwikkelaars kunnen toobuild beveiligde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="6fa7f-141">Voor meer informatie gaat u naar Hallo [opslag beveiligingshandleiding](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
