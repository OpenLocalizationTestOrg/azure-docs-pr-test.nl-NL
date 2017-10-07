---
title: "aaaAzure voorbeeldscript CLI - momentopname exporteren/kopiëren als VHD tooa storage-account in andere regio | Microsoft Docs"
description: "Azure CLI-voorbeeldscript - momentopname exporteren/kopiëren als VHD tooa opslagaccount in dezelfde of een ander abonnement"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Export/exemplaar beheerde momentopnamen als VHD tooa storage-account in andere regio met CLI

Dit script exporteert u een beheerde momentopname tooa storage-account in andere regio. Deze genereert eerst Hallo SAS-URI van de momentopname Hallo en gebruikt vervolgens toocopy het tooa storage-account in andere regio. Gebruik deze back-up toomaintain script beheerde schijven in andere regio voor herstel na noodgevallen. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van opdrachten toogenerate na SAS-URI voor een beheerde momentopnamen en kopieën op Hallo momentopname tooa storage-account met behulp van SAS-URI. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ momentopname toegang verlenen](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Genereert alleen-lezen SA's dat is gebruikt toocopy onderliggende VHD-bestand tooa storage-account of download deze tooon-premises  |
| [start AZ storage-blob kopiëren](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Een blob asynchroon opgehaald uit één storage account tooanother |

## <a name="next-steps"></a>Volgende stappen

[Een beheerde schijf vanaf een VHD maken](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Een virtuele machine maken van een beheerde schijf](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
