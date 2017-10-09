---
title: een VPN-gatewayverbinding aaaVerify | Microsoft Docs
description: Dit artikel laat zien hoe tooverify a virtual network-VPN-gatewayverbinding.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a>Een VPN-Gateway-verbinding controleren

Dit artikel ziet u hoe tooverify een VPN-gatewayverbinding voor zowel klassieke Hallo als Resource Manager-implementatiemodel.

## <a name="azure-portal"></a>Azure Portal

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a>PowerShell

tooverify een VPN-gatewayverbinding voor implementatie van Resource Manager Hallo model met behulp van PowerShell, installeert u de meest recente versie Hallo Hallo [Azure Resource Manager PowerShell-cmdlets](/powershell/azure/overview).

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a>Azure CLI

tooverify een VPN-gatewayverbinding voor implementatie van Resource Manager Hallo model met Azure CLI, installeert u de meest recente versie Hallo Hallo [CLI-opdrachten](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 of hoger).

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a>Azure-portal (klassiek)

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a>PowerShell (klassiek)

tooverify uw VPN-gatewayverbinding voor Hallo-classic deployment model met behulp van PowerShell, de meest recente versies Hallo Hallo Azure PowerShell-cmdlets installeren. Ervoor toodownload en installeer Hallo worden [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module. Gebruik de Add-AzureAccount toolog in toohello klassieke implementatiemodel.

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a>Volgende stappen

* U kunt virtuele netwerken van virtuele machines tooyour toevoegen. Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.
