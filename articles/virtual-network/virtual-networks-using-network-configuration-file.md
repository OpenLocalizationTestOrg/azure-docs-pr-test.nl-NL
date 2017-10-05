---
title: Een Azure-netwerk (klassiek) - configuratiebestand netwerk configureren | Microsoft Docs
description: Informatie over het maken en wijzigen van virtuele netwerken (klassiek) te exporteren en importeren van een configuratiebestand netwerk wijzigen.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="0b698-103">Een virtueel netwerk (klassiek) met een configuratiebestand netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="0b698-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0b698-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b698-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0b698-105">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0b698-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="0b698-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-implementatiemodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0b698-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="0b698-107">U kunt maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand met de Azure-opdrachtregelinterface (CLI) 1.0 of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b698-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="0b698-108">U kunt maken of wijzigen van een virtueel netwerk via het Azure Resource Manager-implementatiemodel met een netwerk configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0b698-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="0b698-109">U niet de Azure portal maken of wijzigen van een virtueel netwerk (klassiek), met een configuratiebestand netwerk, maar u kunt de Azure portal een virtueel netwerk (klassiek) maken zonder gebruik van een configuratiebestand netwerk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0b698-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="0b698-110">Maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand moet exporteren en importeren van het bestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0b698-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="0b698-111"><a name="export"></a>Een netwerk-configuratiebestand exporteren</span><span class="sxs-lookup"><span data-stu-id="0b698-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="0b698-112">U kunt PowerShell of Azure CLI gebruiken voor het exporteren van een netwerk-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0b698-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="0b698-113">PowerShell exporteert een XML-bestand, terwijl de Azure CLI een json-bestand exporteert.</span><span class="sxs-lookup"><span data-stu-id="0b698-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="0b698-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b698-114">PowerShell</span></span>
 
1. <span data-ttu-id="0b698-115">[Azure PowerShell installeren en aanmelden bij Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b698-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0b698-116">Wijzig de directory (en zorg ervoor dat deze bestaat) en de bestandsnaam in de volgende opdracht naar wens, voer de opdracht voor het exporteren van het configuratiebestand van het netwerk:</span><span class="sxs-lookup"><span data-stu-id="0b698-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0b698-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b698-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0b698-118">[Installeer de Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b698-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0b698-119">De resterende stappen vanaf een opdrachtprompt Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="0b698-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0b698-120">Meld u aan bij Azure door te voeren de `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0b698-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="0b698-121">Zorg ervoor dat u zich in de asm-modus door te voeren de `azure config mode asm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0b698-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0b698-122">Wijzig de directory (en zorg ervoor dat deze bestaat) en de bestandsnaam in de volgende opdracht naar wens, voer de opdracht voor het exporteren van het configuratiebestand van het netwerk:</span><span class="sxs-lookup"><span data-stu-id="0b698-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="0b698-123">Maken of een configuratiebestand netwerk wijzigen</span><span class="sxs-lookup"><span data-stu-id="0b698-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="0b698-124">Een configuratiebestand netwerk is een XML-bestand (als u PowerShell) of een json-bestand (als u de Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="0b698-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="0b698-125">U kunt het bestand in een tekst- of XML-/ json-editor kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="0b698-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="0b698-126">De [netwerk-instellingen voor het configuratiebestand schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) artikel bevat informatie voor alle instellingen.</span><span class="sxs-lookup"><span data-stu-id="0b698-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="0b698-127">Zie voor aanvullende uitleg van de instellingen [virtuele netwerken en instellingen weergeven](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="0b698-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="0b698-128">De wijzigingen die u in het bestand aanbrengt:</span><span class="sxs-lookup"><span data-stu-id="0b698-128">The changes you make to the file:</span></span>

- <span data-ttu-id="0b698-129">Moet voldoen aan het schema of het importeren van die het configuratiebestand van het netwerk mislukt.</span><span class="sxs-lookup"><span data-stu-id="0b698-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="0b698-130">Overschrijf de bestaande netwerkinstellingen voor uw abonnement, dus Wees daarom uiterst voorzichtig als u wijzigingen aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="0b698-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="0b698-131">Verwijs bijvoorbeeld naar de configuratiebestanden van de voorbeeld-netwerk die volgen.</span><span class="sxs-lookup"><span data-stu-id="0b698-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="0b698-132">Stel het oorspronkelijke bestand bevat twee **VirtualNetworkSite** exemplaren en u gewijzigd, zoals wordt weergegeven in de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="0b698-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="0b698-133">Wanneer u het bestand importeert, Azure worden verwijderd van het virtuele netwerk voor de **VirtualNetworkSite** exemplaar dat u in het bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0b698-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="0b698-134">Dit scenario vereenvoudigde wordt ervan uitgegaan dat er zijn geen bronnen in het virtuele netwerk alsof er, het virtuele netwerk kan niet worden verwijderd en het importeren mislukt.</span><span class="sxs-lookup"><span data-stu-id="0b698-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b698-135">Azure overweegt een subnet met iets geïmplementeerd als **gebruikt**.</span><span class="sxs-lookup"><span data-stu-id="0b698-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="0b698-136">Wanneer een subnet gebruikt wordt, kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0b698-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="0b698-137">Voordat u informatie over het subnet in een configuratiebestand netwerk wijzigt, verplaatst u alles wat u hebt geïmplementeerd op het subnet moet een ander subnet dat is niet wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0b698-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="0b698-138">Zie [een virtuele machine of Rolinstantie verplaatsen naar een ander Subnet](virtual-networks-move-vm-role-to-subnet.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0b698-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="0b698-139">XML-voorbeeld voor gebruik met PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b698-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="0b698-140">Het volgende configuratiebestand van de voorbeeld-netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in de *VS-Oost* Azure de regio.</span><span class="sxs-lookup"><span data-stu-id="0b698-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="0b698-141">Het virtuele netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0b698-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="0b698-142">Als het netwerk-configuratiebestand dat u hebt geëxporteerd geen inhoud bevat, kunt u de XML in het vorige voorbeeld kopieert en plakt u deze in een nieuw bestand.</span><span class="sxs-lookup"><span data-stu-id="0b698-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="0b698-143">Voorbeeld JSON voor gebruik met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b698-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="0b698-144">Het volgende configuratiebestand van de voorbeeld-netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in de *VS-Oost* Azure de regio.</span><span class="sxs-lookup"><span data-stu-id="0b698-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="0b698-145">Het virtuele netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0b698-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="0b698-146">Als het netwerk-configuratiebestand dat u hebt geëxporteerd geen inhoud bevat, kunt u kopiëren van de json in het vorige voorbeeld en plak deze in een nieuw bestand.</span><span class="sxs-lookup"><span data-stu-id="0b698-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="0b698-147"><a name="import"></a>Een configuratiebestand netwerk importeren</span><span class="sxs-lookup"><span data-stu-id="0b698-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="0b698-148">U kunt PowerShell of Azure CLI gebruiken voor het importeren van een netwerk-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0b698-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="0b698-149">PowerShell importeert een XML-bestand, terwijl de Azure CLI een json-bestand importeert.</span><span class="sxs-lookup"><span data-stu-id="0b698-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="0b698-150">Als het importeren is mislukt, moet u bevestigen dat het bestand voldoet aan de [network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b698-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="0b698-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b698-151">PowerShell</span></span>
 
1. <span data-ttu-id="0b698-152">[Azure PowerShell installeren en aanmelden bij Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b698-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0b698-153">Wijzig de map en bestandsnaam in de volgende opdracht als nodig Voer vervolgens de opdracht voor het importeren van het configuratiebestand van het netwerk:</span><span class="sxs-lookup"><span data-stu-id="0b698-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0b698-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b698-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0b698-155">[Installeer de Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b698-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0b698-156">De resterende stappen vanaf een opdrachtprompt Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="0b698-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0b698-157">Meld u aan bij Azure door te voeren de `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0b698-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="0b698-158">Zorg ervoor dat u zich in de asm-modus door te voeren de `azure config mode asm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0b698-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0b698-159">Wijzig de map en bestandsnaam in de volgende opdracht als nodig Voer vervolgens de opdracht voor het importeren van het configuratiebestand van het netwerk:</span><span class="sxs-lookup"><span data-stu-id="0b698-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
