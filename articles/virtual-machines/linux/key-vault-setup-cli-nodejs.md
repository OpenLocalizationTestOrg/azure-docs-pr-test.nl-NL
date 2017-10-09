---
title: aaaSet up Sleutelkluis voor virtuele Linux-machines Hello Azure CLI 1.0 | Microsoft Docs
description: Hoe Hallo tooset up Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager met Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="60b5d-103">Sleutelkluis instellen voor virtuele machines in Azure Resource Manager met hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60b5d-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="60b5d-104">In Azure Resource Manager-stack hello, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de resourceprovider Hallo van Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="60b5d-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="60b5d-105">Zie toolearn meer informatie over Azure Key Vault [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="60b5d-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="60b5d-106">Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager *EnabledForDeployment* eigenschap op Sleutelkluis tootrue moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="60b5d-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="60b5d-107">U kunt dit doen in verschillende clients.</span><span class="sxs-lookup"><span data-stu-id="60b5d-107">You can do this in various clients.</span></span> <span data-ttu-id="60b5d-108">Dit artikel ziet u hoe tooset up Sleutelkluis voor gebruik met Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="60b5d-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="60b5d-109">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="60b5d-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="60b5d-110">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak voltooien</span><span class="sxs-lookup"><span data-stu-id="60b5d-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="60b5d-111">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="60b5d-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="60b5d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="60b5d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="60b5d-113">CLI-1.0 tooset up Sleutelkluis gebruiken</span><span class="sxs-lookup"><span data-stu-id="60b5d-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="60b5d-114">toocreate een sleutelkluis met behulp van Hallo-opdrachtregelinterface (CLI), Zie [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="60b5d-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="60b5d-115">Voor CLI 1.0 hebt u toocreate hello sleutelkluis voordat u beleid voor Hallo implementatie toewijst.</span><span class="sxs-lookup"><span data-stu-id="60b5d-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="60b5d-116">U kunt vervolgens Hallo beleid met behulp van de volgende opdracht Hallo toewijzen:</span><span class="sxs-lookup"><span data-stu-id="60b5d-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="60b5d-117">Gebruik sjablonen tooset up Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="60b5d-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="60b5d-118">Wanneer u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource.</span><span class="sxs-lookup"><span data-stu-id="60b5d-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="60b5d-119">Zie voor andere opties die u configureren kunt wanneer u een sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="60b5d-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
