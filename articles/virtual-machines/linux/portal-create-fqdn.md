---
title: aaaCreate FQDN voor een Linux-VM in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate een FQDN-naam of FQDN voor een Resource Manager op basis van virtuele machine in hello Azure-portal.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal voor een Linux-VM

Wanneer u een virtuele machine (VM) maakt in Hallo [Azure-portal](https://portal.azure.com), een openbare IP-resource voor Hallo virtuele machine automatisch wordt gemaakt. U gebruikt dit IP-adres tooremotely toegang Hallo VM. Hoewel het Hallo-portal maakt geen een [volledig gekwalificeerde domeinnaam](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), of de FQDN-naam, kunt u een toevoegen wanneer hello VM is gemaakt. Dit artikel wordt gedemonstreerd Hallo stappen toocreate een DNS-naam of FQDN-naam.

## <a name="create-a-fqdn"></a>Maken van een FQDN-naam
In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt. Indien nodig, kunt u [maken van een virtuele machine in Hallo portal](quick-create-portal.md) of [Hello Azure CLI](quick-create-cli.md). Volg deze stappen nadat uw virtuele machine actief is:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

U kunt nu verbinding op afstand toohello VM die gebruikmaakt van de DNS-naam, zoals met `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Volgende stappen
Nu dat uw virtuele machine een openbare IP-adres en DNS-naam heeft, kunt u implementeren algemene toepassingsframeworks of -services zoals nginx, MongoDB, Docker, enzovoort.

U kunt ook meer informatie over [met Resource Manager](../../azure-resource-manager/resource-group-overview.md) voor tips over het bouwen van uw Azure-implementaties.

