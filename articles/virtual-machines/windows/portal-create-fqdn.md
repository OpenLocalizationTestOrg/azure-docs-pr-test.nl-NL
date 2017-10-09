---
title: aaaCreate FQDN-naam voor een virtuele machine van Windows in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate een FQDN-naam of FQDN voor een Resource Manager op basis van virtuele machine in hello Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal voor een virtuele machine van Windows

Wanneer u een virtuele machine (VM) maakt in Hallo [Azure-portal](https://portal.azure.com), een openbare IP-resource voor Hallo virtuele machine automatisch wordt gemaakt. U gebruikt dit IP-adres tooremotely toegang Hallo VM. Hoewel het Hallo-portal maakt geen een [volledig gekwalificeerde domeinnaam](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), of de FQDN-naam, kunt u een zodra hello VM is gemaakt. Dit artikel wordt gedemonstreerd Hallo stappen toocreate een DNS-naam of FQDN-naam.

## <a name="create-a-fqdn"></a>Maken van een FQDN-naam
In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt. Indien nodig, kunt u [maken van een virtuele machine in Hallo portal](quick-create-portal.md) of [met Azure PowerShell](quick-create-powershell.md). Volg deze stappen nadat uw virtuele machine actief is:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

U kunt nu verbinding op afstand toohello VM die gebruikmaakt van deze DNS-naam, zoals voor Remote Desktop Protocol (RDP).

## <a name="next-steps"></a>Volgende stappen
Nu dat uw virtuele machine een openbare IP-adres en DNS-naam heeft, kunt u algemene toepassingsframeworks of services, zoals IIS, SQL en SharePoint kunt implementeren.

U kunt ook meer informatie over [met Resource Manager](../../azure-resource-manager/resource-group-overview.md) voor tips over het bouwen van uw Azure-implementaties.

