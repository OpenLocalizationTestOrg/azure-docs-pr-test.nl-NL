---
title: PowerShell-voorbeeldscript - aaaAzure versleutelen van een virtuele machine van Windows | Microsoft Docs
description: Azure PowerShell-Script steekproef - versleutelen van een Windows VM
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="99fc1-103">Versleutelen van een virtuele Windows-machine met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="99fc1-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="99fc1-104">Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Windows-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="99fc1-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="99fc1-105">Hallo VM wordt vervolgens versleuteld met de versleutelingssleutel Hallo van Sleutelkluis en de service principal referenties.</span><span class="sxs-lookup"><span data-stu-id="99fc1-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="99fc1-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="99fc1-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="99fc1-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="99fc1-107">Clean up deployment</span></span> 

<span data-ttu-id="99fc1-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99fc1-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="99fc1-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="99fc1-109">Script explanation</span></span>

<span data-ttu-id="99fc1-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="99fc1-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="99fc1-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="99fc1-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="99fc1-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="99fc1-112">Command</span></span> | <span data-ttu-id="99fc1-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="99fc1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="99fc1-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="99fc1-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="99fc1-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="99fc1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="99fc1-116">Nieuwe AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="99fc1-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="99fc1-117">Hiermee maakt u een beveiligde gegevens van Azure Sleutelkluis toostore zoals versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="99fc1-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="99fc1-118">-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="99fc1-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="99fc1-119">Maakt een versleutelingssleutel in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="99fc1-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="99fc1-120">Nieuwe AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="99fc1-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="99fc1-121">Hiermee maakt u een Azure Active Directory-service principal toosecurely verifiëren en toegang tooencryption sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="99fc1-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="99fc1-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="99fc1-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="99fc1-123">Machtigingen op Hallo Sleutelkluis toogrant Hallo service principal tooencryption toegangstoetsen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="99fc1-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="99fc1-124">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="99fc1-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="99fc1-125">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="99fc1-125">Creates a subnet configuration.</span></span> <span data-ttu-id="99fc1-126">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="99fc1-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="99fc1-127">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="99fc1-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="99fc1-128">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="99fc1-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="99fc1-129">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="99fc1-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="99fc1-130">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="99fc1-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="99fc1-131">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="99fc1-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="99fc1-132">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="99fc1-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="99fc1-133">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99fc1-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="99fc1-134">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="99fc1-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="99fc1-135">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="99fc1-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="99fc1-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="99fc1-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="99fc1-137">Hiermee haalt u informatie over het subnet.</span><span class="sxs-lookup"><span data-stu-id="99fc1-137">Gets subnet information.</span></span> <span data-ttu-id="99fc1-138">Deze informatie wordt gebruikt bij het maken van een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="99fc1-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="99fc1-139">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="99fc1-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="99fc1-140">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="99fc1-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="99fc1-141">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="99fc1-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="99fc1-142">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="99fc1-142">Creates a VM configuration.</span></span> <span data-ttu-id="99fc1-143">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="99fc1-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="99fc1-144">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="99fc1-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="99fc1-145">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="99fc1-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="99fc1-146">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="99fc1-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="99fc1-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="99fc1-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="99fc1-148">Vereiste informatie op Hallo Sleutelkluis opgehaald</span><span class="sxs-lookup"><span data-stu-id="99fc1-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="99fc1-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="99fc1-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="99fc1-150">Hiermee schakelt u versleuteling op een virtuele machine met behulp van de principal Servicereferenties Hallo en versleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="99fc1-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="99fc1-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="99fc1-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="99fc1-152">Geeft de status Hallo Hallo versleutelingsproces VM.</span><span class="sxs-lookup"><span data-stu-id="99fc1-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="99fc1-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="99fc1-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="99fc1-154">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="99fc1-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99fc1-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99fc1-155">Next steps</span></span>

<span data-ttu-id="99fc1-156">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99fc1-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="99fc1-157">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99fc1-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
