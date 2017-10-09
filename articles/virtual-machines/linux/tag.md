---
title: aaaHow tootag een virtuele machine van Azure Linux | Microsoft Docs
description: Meer informatie over labels van een Azure Linux virtuele machine in Azure met Resource Manager-implementatiemodel Hallo gemaakt.
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Hoe tootag virtuele Linux-machine in Azure
In dit artikel beschrijft de verschillende manieren tootag virtuele Linux-machine in Azure via Hallo Resource Manager-implementatiemodel. Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst. Azure biedt momenteel ondersteuning voor maximaal too15 labels per resource en resourcegroep. Labels van een resource kunnen worden geplaatst op Hallo moment gemaakt of bestaande resource tooan toegevoegd. Houd er rekening mee,-labels worden ondersteund voor resources die zijn gemaakt via Hallo Resource Manager-implementatiemodel alleen.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Met Azure CLI-tagging
toobegin, moet u Hallo nieuwste [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

U kunt alle eigenschappen weergeven voor een bepaalde virtuele Machine, met inbegrip van Hallo labels, met de volgende opdracht:

        az vm show --resource-group MyResourceGroup --name MyTestVM

een nieuwe VM-tag via hello Azure CLI tooadd, kunt u Hallo `azure vm update` opdracht samen met de parameter tag Hallo **--ingesteld**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

tooremove tags, kunt u Hallo **--verwijderen** parameter in Hallo `azure vm update` opdracht.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


Nu dat we labels tooour resources Azure CLI hebt toegepast en Hallo Portal, eens kijken Hallo gebruik details toosee Hallo labels in facturering Hallo-portal.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over uw Azure-resources te labelen [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [tooorganize labels met behulp van uw Azure-Resources] [ Using Tags tooorganize your Azure Resources].
* toosee hoe labels kunt u uw gebruik van Azure-resources beheren raadpleegt [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
