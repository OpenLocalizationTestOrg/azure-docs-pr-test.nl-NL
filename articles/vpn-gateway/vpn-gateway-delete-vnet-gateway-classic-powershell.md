---
title: 'Een virtuele netwerkgateway verwijderen: PowerShell: klassieke Azure Portal | Microsoft Docs'
description: Verwijder de gateway van een virtueel netwerk met PowerShell in het klassieke implementatiemodel.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="3807f-103">Verwijder de gateway van een virtueel netwerk met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3807f-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3807f-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3807f-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="3807f-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3807f-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="3807f-106">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3807f-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="3807f-107">In dit artikel helpt u bij het verwijderen van een VPN-gateway in het klassieke implementatiemodel met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3807f-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="3807f-108">Nadat de virtuele netwerkgateway is verwijderd, wijzigt u het configuratiebestand netwerk om het verwijderen van elementen die u niet meer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3807f-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="3807f-109"><a name="connect"></a>Stap 1: Verbinding maken met Azure</span><span class="sxs-lookup"><span data-stu-id="3807f-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="3807f-110">1. Installeer de meest recente PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3807f-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="3807f-111">Download en installeer de nieuwste versie van de Azure Service Management (SM) PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3807f-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="3807f-112">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3807f-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="3807f-113">2. Verbinding maken met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3807f-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="3807f-114">Open de PowerShell-console met verhoogde rechten en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="3807f-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="3807f-115">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="3807f-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="3807f-116"><a name="export"></a>Stap 2: Exporteren en het configuratiebestand van het netwerk weergeven</span><span class="sxs-lookup"><span data-stu-id="3807f-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="3807f-117">Maak een map op de computer en exporteer vervolgens het netwerkconfiguratiebestand naar de map.</span><span class="sxs-lookup"><span data-stu-id="3807f-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="3807f-118">U dit bestand op beide bekijkt u de huidige configuratie-informatie en om te wijzigen van de netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="3807f-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="3807f-119">In dit voorbeeld wordt het netwerkconfiguratiebestand geëxporteerd naar C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="3807f-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="3807f-120">Open het bestand met een teksteditor en de naam voor het klassieke VNet weergeven.</span><span class="sxs-lookup"><span data-stu-id="3807f-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="3807f-121">Wanneer u een VNet in de Azure portal maakt, is de volledige naam die gebruikmaakt van Azure niet zichtbaar in de portal.</span><span class="sxs-lookup"><span data-stu-id="3807f-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="3807f-122">Een VNet dat wordt weergegeven naam 'ClassicVNet1' in de Azure portal kan bijvoorbeeld een veel langer naam hebben in het configuratiebestand van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3807f-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="3807f-123">De naam kan als volgt uitzien: 'Groep ClassicRG1 ClassicVNet1'.</span><span class="sxs-lookup"><span data-stu-id="3807f-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="3807f-124">Virtuele netwerken worden vermeld als **' VirtualNetworkSite name ='**.</span><span class="sxs-lookup"><span data-stu-id="3807f-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="3807f-125">De namen in het configuratiebestand van het netwerk gebruiken bij het uitvoeren van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3807f-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="3807f-126"><a name="delete"></a>Stap 3: De virtuele netwerkgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="3807f-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="3807f-127">Wanneer u een virtuele netwerkgateway verwijdert, worden alle verbindingen met het VNet via de gateway verbroken.</span><span class="sxs-lookup"><span data-stu-id="3807f-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="3807f-128">Als u P2S-clients die zijn verbonden met het VNet hebt, moet het worden beëindigd zonder waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3807f-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="3807f-129">In dit voorbeeld wordt de virtuele netwerkgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3807f-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="3807f-130">Controleer of u de volledige naam van het virtuele netwerk van het configuratiebestand van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3807f-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="3807f-131">Als dit lukt, ziet u het rendement:</span><span class="sxs-lookup"><span data-stu-id="3807f-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="3807f-132"><a name="modify"></a>Stap 4: Wijzig het configuratiebestand van het netwerk</span><span class="sxs-lookup"><span data-stu-id="3807f-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="3807f-133">Wanneer u een virtuele netwerkgateway verwijdert, wijzig de cmdlet niet het configuratiebestand van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3807f-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="3807f-134">U moet het bestand om te verwijderen van de elementen die niet langer worden gebruikt te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3807f-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="3807f-135">De volgende secties helpen u Wijzig het netwerk-configuratiebestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="3807f-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="3807f-136"><a name="lnsref"></a>Verwijzingen naar lokale netwerksites</span><span class="sxs-lookup"><span data-stu-id="3807f-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="3807f-137">Voor het verwijderen van de site-naslaginformatie configuratiewijzigingen aanbrengen in **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="3807f-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="3807f-138">Verwijderen van een lokale site verwijzing triggers Azure een tunnel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3807f-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="3807f-139">Afhankelijk van de configuratie die u hebt gemaakt, hebt u geen een **LocalNetworkSiteRef** vermeld.</span><span class="sxs-lookup"><span data-stu-id="3807f-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="3807f-140">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3807f-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="3807f-141"><a name="lns"></a>Lokale netwerksites</span><span class="sxs-lookup"><span data-stu-id="3807f-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="3807f-142">Verwijder alle lokale sites die u niet meer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3807f-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="3807f-143">Afhankelijk van de configuratie die u hebt gemaakt, is het mogelijk dat u hebt geen een **LocalNetworkSite** vermeld.</span><span class="sxs-lookup"><span data-stu-id="3807f-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="3807f-144">In dit voorbeeld verwijderd we alleen Site3.</span><span class="sxs-lookup"><span data-stu-id="3807f-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="3807f-145"><a name="clientaddresss"></a>Client-adresgroep</span><span class="sxs-lookup"><span data-stu-id="3807f-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="3807f-146">Als u een P2S-verbinding had uw vnet, hebt u een **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="3807f-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="3807f-147">Verwijder de client-adresgroepen die overeenkomen met de virtuele netwerkgateway die u hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3807f-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="3807f-148">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3807f-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="3807f-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="3807f-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="3807f-150">Verwijder de **GatewaySubnet** die overeenkomt met het VNet.</span><span class="sxs-lookup"><span data-stu-id="3807f-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="3807f-151">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3807f-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="3807f-152"><a name="upload"></a>Stap 5: Upload het configuratiebestand van het netwerk</span><span class="sxs-lookup"><span data-stu-id="3807f-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="3807f-153">Sla uw wijzigingen en het configuratiebestand van het netwerk te uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3807f-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="3807f-154">Zorg ervoor dat u het bestandspad dat nodig is voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3807f-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="3807f-155">Als dit lukt, ziet u het retourtype iets dergelijks zijn op dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3807f-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded