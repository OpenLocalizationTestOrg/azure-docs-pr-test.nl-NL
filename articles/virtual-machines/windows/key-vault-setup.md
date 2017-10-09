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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Sleutelkluis instellen voor virtuele machines in Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

In Azure Resource Manager-stack, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de resourceprovider Hallo van Sleutelkluis. toolearn meer informatie over de Sleutelkluis, Zie [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager **EnabledForDeployment** eigenschap op Sleutelkluis tootrue moet worden ingesteld. U kunt dit doen in verschillende clients.
> 2. Hallo Sleutelkluis behoeften toobe gemaakt in Hallo hetzelfde abonnement en dezelfde locatie als Hallo van virtuele Machine.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Gebruik PowerShell tooset up Sleutelkluis
toocreate een sleutelkluis met behulp van PowerShell, Zie [aan de slag met Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).

Voor nieuwe sleutelkluizen, kunt u deze PowerShell-cmdlet:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Voor bestaande sleutelkluizen, kunt u deze PowerShell-cmdlet:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Ons CLI tooset up Sleutelkluis
toocreate een sleutelkluis met behulp van Hallo-opdrachtregelinterface (CLI), Zie [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Voor CLI hebt u toocreate hello sleutelkluis voordat u beleid voor Hallo implementatie toewijst. U kunt dit doen met behulp van de volgende opdracht Hallo:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Gebruik sjablonen tooset up Sleutelkluis
Terwijl u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource.

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

Zie voor andere opties die u configureren kunt wanneer u een sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
