---
title: aaaSet up Key Vault voor Windows-VM's in Azure Resource Manager | Microsoft Docs
description: Hoe tooset up Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="4b3e8-103">Sleutelkluis instellen voor virtuele machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b3e8-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="4b3e8-104">In Azure Resource Manager-stack, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de resourceprovider Hallo van Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="4b3e8-105">toolearn meer informatie over de Sleutelkluis, Zie [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="4b3e8-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="4b3e8-106">Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager **EnabledForDeployment** eigenschap op Sleutelkluis tootrue moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="4b3e8-107">U kunt dit doen in verschillende clients.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="4b3e8-108">Hallo Sleutelkluis behoeften toobe gemaakt in Hallo hetzelfde abonnement en dezelfde locatie als Hallo van virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="4b3e8-109">Gebruik PowerShell tooset up Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="4b3e8-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="4b3e8-110">toocreate een sleutelkluis met behulp van PowerShell, Zie [aan de slag met Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="4b3e8-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="4b3e8-111">Voor nieuwe sleutelkluizen, kunt u deze PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b3e8-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="4b3e8-112">Voor bestaande sleutelkluizen, kunt u deze PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b3e8-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="4b3e8-113">Ons CLI tooset up Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="4b3e8-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="4b3e8-114">toocreate een sleutelkluis met behulp van Hallo-opdrachtregelinterface (CLI), Zie [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="4b3e8-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="4b3e8-115">Voor CLI hebt u toocreate hello sleutelkluis voordat u beleid voor Hallo implementatie toewijst.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="4b3e8-116">U kunt dit doen met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4b3e8-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="4b3e8-117">Gebruik sjablonen tooset up Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="4b3e8-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="4b3e8-118">Terwijl u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource.</span><span class="sxs-lookup"><span data-stu-id="4b3e8-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="4b3e8-119">Zie voor andere opties die u configureren kunt wanneer u een sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="4b3e8-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
