---
title: Instellen van de Sleutelkluis voor Windows-machines in Azure Resource Manager | Microsoft Docs
description: Het instellen van de Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager.
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
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="6eeb8-103">Sleutelkluis instellen voor virtuele machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6eeb8-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="6eeb8-104">In Azure Resource Manager-stack, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de bronprovider van de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="6eeb8-105">Zie voor meer informatie over Sleutelkluis, [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6eeb8-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="6eeb8-106">In de volgorde voor Sleutelkluis moet worden gebruikt met virtuele machines van Azure Resource Manager, de **EnabledForDeployment** eigenschap voor Sleutelkluis moet zijn ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="6eeb8-107">U kunt dit doen in verschillende clients.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="6eeb8-108">De Sleutelkluis moet worden gemaakt in hetzelfde abonnement en dezelfde locatie als de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="6eeb8-109">PowerShell gebruiken voor het instellen van de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="6eeb8-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="6eeb8-110">Zie voor informatie over het maken van een sleutelkluis met behulp van PowerShell [aan de slag met Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="6eeb8-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="6eeb8-111">Voor nieuwe sleutelkluizen, kunt u deze PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6eeb8-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="6eeb8-112">Voor bestaande sleutelkluizen, kunt u deze PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6eeb8-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="6eeb8-113">Ons CLI voor het instellen van de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="6eeb8-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="6eeb8-114">Zie voor informatie over het maken van een sleutelkluis via de opdrachtregelinterface (CLI) [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="6eeb8-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="6eeb8-115">U hebt de sleutelkluis maken voordat u het beleid voor de implementatie toewijzen voor CLI.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="6eeb8-116">U gebruikt hiervoor de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6eeb8-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="6eeb8-117">Sjablonen gebruiken voor het instellen van de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="6eeb8-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="6eeb8-118">Terwijl u een sjabloon gebruikt, moet u de `enabledForDeployment` eigenschap `true` voor de Sleutelkluis-resource.</span><span class="sxs-lookup"><span data-stu-id="6eeb8-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="6eeb8-119">Zie voor andere opties die u configureren kunt wanneer u een sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="6eeb8-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
