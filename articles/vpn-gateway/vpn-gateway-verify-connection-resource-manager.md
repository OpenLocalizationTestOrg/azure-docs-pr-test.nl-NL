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
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="0643c-103">Een VPN-Gateway-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="0643c-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="0643c-104">Dit artikel ziet u hoe tooverify een VPN-gatewayverbinding voor zowel klassieke Hallo als Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0643c-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="0643c-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0643c-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="0643c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0643c-106">PowerShell</span></span>

<span data-ttu-id="0643c-107">tooverify een VPN-gatewayverbinding voor implementatie van Resource Manager Hallo model met behulp van PowerShell, installeert u de meest recente versie Hallo Hallo [Azure Resource Manager PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0643c-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="0643c-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0643c-108">Azure CLI</span></span>

<span data-ttu-id="0643c-109">tooverify een VPN-gatewayverbinding voor implementatie van Resource Manager Hallo model met Azure CLI, installeert u de meest recente versie Hallo Hallo [CLI-opdrachten](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 of hoger).</span><span class="sxs-lookup"><span data-stu-id="0643c-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="0643c-110">Azure-portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="0643c-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="0643c-111">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="0643c-111">PowerShell (classic)</span></span>

<span data-ttu-id="0643c-112">tooverify uw VPN-gatewayverbinding voor Hallo-classic deployment model met behulp van PowerShell, de meest recente versies Hallo Hallo Azure PowerShell-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="0643c-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0643c-113">Ervoor toodownload en installeer Hallo worden [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span><span class="sxs-lookup"><span data-stu-id="0643c-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="0643c-114">Gebruik de Add-AzureAccount toolog in toohello klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0643c-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0643c-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0643c-115">Next steps</span></span>

* <span data-ttu-id="0643c-116">U kunt virtuele netwerken van virtuele machines tooyour toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0643c-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="0643c-117">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="0643c-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
