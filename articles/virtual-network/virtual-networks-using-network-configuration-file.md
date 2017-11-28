---
title: een Azure-netwerk (klassiek) - configuratiebestand netwerk aaaConfigure | Microsoft Docs
description: Meer informatie over hoe toocreate en wijzigen van virtuele netwerken (klassiek) te exporteren en importeren van een configuratiebestand netwerk wijzigen.
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
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="8ab76-103">Een virtueel netwerk (klassiek) met een configuratiebestand netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="8ab76-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ab76-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ab76-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8ab76-105">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ab76-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8ab76-106">Microsoft raadt aan dat de meeste nieuwe implementaties Hallo Resource Manager-implementatiemodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="8ab76-107">U kunt maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand met hello Azure-opdrachtregelinterface (CLI) 1.0 of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ab76-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="8ab76-108">U kunt maken of wijzigen van een virtueel netwerk via hello Azure Resource Manager-implementatiemodel met een netwerk configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8ab76-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="8ab76-109">U kan hello Azure portal toocreate gebruiken of een virtueel netwerk (klassiek) met een configuratiebestand netwerk wijzigen, maar u kunt Hallo toocreate met Azure portal een virtueel netwerk (klassiek), zonder gebruik van een netwerk-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8ab76-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="8ab76-110">Maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand vereist exporteren, wijzigen en het Hallo-bestand te importeren.</span><span class="sxs-lookup"><span data-stu-id="8ab76-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="8ab76-111"><a name="export"></a>Een netwerk-configuratiebestand exporteren</span><span class="sxs-lookup"><span data-stu-id="8ab76-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="8ab76-112">U kunt PowerShell of hello Azure CLI tooexport een configuratiebestand netwerk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="8ab76-113">PowerShell exporteert een XML-bestand, terwijl hello Azure CLI een json-bestand exporteert.</span><span class="sxs-lookup"><span data-stu-id="8ab76-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="8ab76-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab76-114">PowerShell</span></span>
 
1. <span data-ttu-id="8ab76-115">[Azure PowerShell installeren en meld u aan tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ab76-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="8ab76-116">Wijzig de directory hello (en zorg ervoor dat deze bestaat) en de bestandsnaam in Hallo de volgende opdracht als de gewenste en vervolgens uitvoeren Hallo opdracht tooexport Hallo netwerk configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="8ab76-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="8ab76-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab76-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="8ab76-118">[Installeer Azure CLI 1.0 Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ab76-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8ab76-119">Hallo resterende stappen vanaf een opdrachtprompt Azure CLI 1.0 voltooien.</span><span class="sxs-lookup"><span data-stu-id="8ab76-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="8ab76-120">Aanmelden tooAzure hiertoe Hallo `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8ab76-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="8ab76-121">Of u in de asm-modus hiertoe Hallo `azure config mode asm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8ab76-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="8ab76-122">Wijzig de directory hello (en zorg ervoor dat deze bestaat) en de bestandsnaam in Hallo de volgende opdracht als de gewenste en vervolgens uitvoeren Hallo opdracht tooexport Hallo netwerk configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="8ab76-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="8ab76-123">Maken of een configuratiebestand netwerk wijzigen</span><span class="sxs-lookup"><span data-stu-id="8ab76-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="8ab76-124">Een configuratiebestand netwerk is een XML-bestand (als u PowerShell) of een json-bestand (als u hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="8ab76-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="8ab76-125">Hallo-bestand in een tekst- of XML-/ json-editor kunt u bewerken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="8ab76-126">Hallo [netwerk-instellingen voor het configuratiebestand schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) artikel bevat informatie voor alle instellingen.</span><span class="sxs-lookup"><span data-stu-id="8ab76-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="8ab76-127">Zie voor aanvullende uitleg van Hallo instellingen [virtuele netwerken en instellingen weergeven](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="8ab76-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="8ab76-128">Hallo-wijzigingen die u aanbrengt toohello bestand:</span><span class="sxs-lookup"><span data-stu-id="8ab76-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="8ab76-129">Moet in overeenstemming met de Hallo schema of importeren Hallo netwerk configuratiebestand zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="8ab76-130">Overschrijf de bestaande netwerkinstellingen voor uw abonnement, dus Wees daarom uiterst voorzichtig als u wijzigingen aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="8ab76-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="8ab76-131">Verwijs bijvoorbeeld naar Hallo voorbeeld netwerk configuratiebestanden die volgen.</span><span class="sxs-lookup"><span data-stu-id="8ab76-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="8ab76-132">Zeg Hallo oorspronkelijke bestand bevat twee **VirtualNetworkSite** exemplaren en u gewijzigd, zoals getoond in Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8ab76-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="8ab76-133">Als u Hallo bestand importeert, Azure Hallo virtueel netwerk voor Hallo verwijdert **VirtualNetworkSite** exemplaar dat u in het Hallo-bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8ab76-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="8ab76-134">Dit scenario vereenvoudigde wordt ervan uitgegaan dat er zijn geen resources zijn in het virtuele netwerk hello, alsof er, Hallo virtueel netwerk kan niet worden verwijderd en Hallo importeren mislukken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ab76-135">Azure overweegt een subnet met iets geïmplementeerd tooit als **gebruikt**.</span><span class="sxs-lookup"><span data-stu-id="8ab76-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="8ab76-136">Wanneer een subnet gebruikt wordt, kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8ab76-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="8ab76-137">Voordat u informatie over het subnet in een configuratiebestand netwerk wijzigt, verplaatst u alles wat u hebt geïmplementeerd toohello subnet tooa ander subnet dat is niet wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8ab76-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="8ab76-138">Zie [verplaatsen van een virtuele machine of Rolinstantie tooa ander Subnet](virtual-networks-move-vm-role-to-subnet.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8ab76-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="8ab76-139">XML-voorbeeld voor gebruik met PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab76-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="8ab76-140">Hallo volgende voorbeeldconfiguratiebestand voor netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in Hallo *VS-Oost* Azure de regio.</span><span class="sxs-lookup"><span data-stu-id="8ab76-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="8ab76-141">Hallo virtueel netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8ab76-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="8ab76-142">Als Hallo netwerk-configuratiebestand exporteren geen inhoud bevat, kunt u Hallo XML in het vorige voorbeeld Hallo kopiëren en plak deze in een nieuw bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab76-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="8ab76-143">Voorbeeld JSON voor gebruik met hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab76-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="8ab76-144">Hallo volgende voorbeeldconfiguratiebestand voor netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in Hallo *VS-Oost* Azure de regio.</span><span class="sxs-lookup"><span data-stu-id="8ab76-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="8ab76-145">Hallo virtueel netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8ab76-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="8ab76-146">Als Hallo netwerk-configuratiebestand exporteren geen inhoud bevat, kunt u Hallo json in het vorige voorbeeld Hallo kopiëren en plak deze in een nieuw bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab76-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="8ab76-147"><a name="import"></a>Een configuratiebestand netwerk importeren</span><span class="sxs-lookup"><span data-stu-id="8ab76-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="8ab76-148">U kunt PowerShell of hello Azure CLI tooimport een configuratiebestand netwerk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ab76-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="8ab76-149">PowerShell importeert een XML-bestand, terwijl hello Azure CLI een json-bestand importeert.</span><span class="sxs-lookup"><span data-stu-id="8ab76-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="8ab76-150">Als Hallo importeren is mislukt, controleert u dat bestand Hallo voldoet aan de Hallo [network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ab76-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="8ab76-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab76-151">PowerShell</span></span>
 
1. <span data-ttu-id="8ab76-152">[Azure PowerShell installeren en meld u aan tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ab76-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="8ab76-153">Hallo directory en de bestandsnaam in Hallo na de opdracht zo nodig wijzigen en voer vervolgens Hallo opdracht tooimport Hallo netwerk configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="8ab76-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="8ab76-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab76-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="8ab76-155">[Installeer Azure CLI 1.0 Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ab76-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8ab76-156">Hallo resterende stappen vanaf een opdrachtprompt Azure CLI 1.0 voltooien.</span><span class="sxs-lookup"><span data-stu-id="8ab76-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="8ab76-157">Aanmelden tooAzure hiertoe Hallo `azure login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8ab76-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="8ab76-158">Of u in de asm-modus hiertoe Hallo `azure config mode asm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8ab76-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="8ab76-159">Hallo directory en de bestandsnaam in Hallo na de opdracht zo nodig wijzigen en voer vervolgens Hallo opdracht tooimport Hallo netwerk configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="8ab76-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
