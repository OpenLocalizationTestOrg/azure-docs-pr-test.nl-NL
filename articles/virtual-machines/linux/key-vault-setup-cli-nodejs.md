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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Sleutelkluis instellen voor virtuele machines in Azure Resource Manager met hello Azure CLI 1.0
In Azure Resource Manager-stack hello, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de resourceprovider Hallo van Sleutelkluis. Zie toolearn meer informatie over Azure Key Vault [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md) Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager *EnabledForDeployment* eigenschap op Sleutelkluis tootrue moet worden ingesteld. U kunt dit doen in verschillende clients. Dit artikel ziet u hoe tooset up Sleutelkluis voor gebruik met Azure Virtual Machines.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak voltooien

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="use-cli-10-tooset-up-key-vault"></a>CLI-1.0 tooset up Sleutelkluis gebruiken
toocreate een sleutelkluis met behulp van Hallo-opdrachtregelinterface (CLI), Zie [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Voor CLI 1.0 hebt u toocreate hello sleutelkluis voordat u beleid voor Hallo implementatie toewijst. U kunt vervolgens Hallo beleid met behulp van de volgende opdracht Hallo toewijzen:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Gebruik sjablonen tooset up Sleutelkluis
Wanneer u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource.

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
