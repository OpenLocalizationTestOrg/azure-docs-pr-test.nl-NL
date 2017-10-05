---
title: Azure Quick Start - Een Windows VM CLI maken | Microsoft Docs
description: Ontdek snel hoe u virtuele Windows-machines maakt met de Azure CLI.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="315a9-103">Een virtuele Windows-machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="315a9-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="315a9-104">De Azure CLI wordt gebruikt voor het maken en beheren van Azure-resources vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="315a9-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="315a9-105">In deze handleiding staat informatie over het gebruik van de Azure CLI om een virtuele machine te implementeren met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="315a9-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="315a9-106">Als de implementatie is voltooid, maken we verbinding met de server en installeren we ISS.</span><span class="sxs-lookup"><span data-stu-id="315a9-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="315a9-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="315a9-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="315a9-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor deze snelstartgids de versie Azure CLI 2.0.4 of hoger uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="315a9-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="315a9-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="315a9-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="315a9-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="315a9-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="315a9-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="315a9-111">Create a resource group</span></span>

<span data-ttu-id="315a9-112">Maak een resourcegroep maken met [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="315a9-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="315a9-113">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="315a9-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="315a9-114">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS Oost*.</span><span class="sxs-lookup"><span data-stu-id="315a9-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="315a9-115">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="315a9-115">Create virtual machine</span></span>

<span data-ttu-id="315a9-116">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="315a9-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="315a9-117">In het volgende voorbeeld wordt een VM met de naam *myVM* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="315a9-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="315a9-118">In dit voorbeeld wordt *azureuser* voor de naam van een gebruiker met beheerdersrechten en *myPassword12* als het wachtwoord gebruikt.</span><span class="sxs-lookup"><span data-stu-id="315a9-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="315a9-119">Werk deze waarden bij met waarden die geschikt zijn voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="315a9-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="315a9-120">Deze waarden zijn nodig als u verbinding maakt met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="315a9-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="315a9-121">Wanneer de virtuele machine is gemaakt, toont de Azure CLI informatie die lijkt op de informatie in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="315a9-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="315a9-122">Noteer het `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="315a9-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="315a9-123">Dit adres wordt gebruikt voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="315a9-123">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="315a9-124">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="315a9-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="315a9-125">Standaard worden alleen RDP-verbindingen toegestaan naar virtuele Windows-machines die zijn geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="315a9-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="315a9-126">Als deze virtuele machine wordt gebruikt als een webserver, moet u poort 80 openen voor verkeer vanaf internet.</span><span class="sxs-lookup"><span data-stu-id="315a9-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="315a9-127">Gebruik de opdracht [az vm open-port](/cli/azure/vm#open-port) om de gewenste poort te openen.</span><span class="sxs-lookup"><span data-stu-id="315a9-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="315a9-128">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="315a9-128">Connect to virtual machine</span></span>

<span data-ttu-id="315a9-129">Gebruik de volgende opdracht om een sessie met een extern bureaublad te starten voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="315a9-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="315a9-130">Vervang het IP-adres door het openbare IP-adres van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="315a9-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="315a9-131">Wanneer u hierom wordt gevraagd, typt u de referenties die zijn gebruikt bij het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="315a9-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="315a9-132">IIS installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="315a9-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="315a9-133">U bent nu aangemeld bij de VM van Azure en er is nog maar één regel code van PowerShell nodig om IIS te installeren en de regel voor de lokale firewall in te schakelen om webverkeer toe te staan.</span><span class="sxs-lookup"><span data-stu-id="315a9-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="315a9-134">Open een PowerShell-prompt en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="315a9-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="315a9-135">De welkomstpagina van IIS weergeven</span><span class="sxs-lookup"><span data-stu-id="315a9-135">View the IIS welcome page</span></span>

<span data-ttu-id="315a9-136">Nu IIS is geïnstalleerd en poort 80 op de virtuele machine is geopend voor toegang vanaf internet, kunt u een webbrowser van uw keuze gebruiken om de standaardwelkomstpagina van IIS weer te geven.</span><span class="sxs-lookup"><span data-stu-id="315a9-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="315a9-137">Zorg ervoor dat u de standaardpagina bezoekt met het openbare IP-adres dat u hierboven hebt gedocumenteerd.</span><span class="sxs-lookup"><span data-stu-id="315a9-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="315a9-139">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="315a9-139">Clean up resources</span></span>

<span data-ttu-id="315a9-140">U kunt de opdracht [az group delete](/cli/azure/group#delete) gebruiken om de resourcegroep, de VM en alle gerelateerde resources te verwijderen wanneer u ze niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="315a9-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="315a9-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="315a9-141">Next steps</span></span>

<span data-ttu-id="315a9-142">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="315a9-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="315a9-143">Voor meer informatie over virtuele machines in Azure, gaat u verder met de zelfstudie voor virtuele Windows-machines.</span><span class="sxs-lookup"><span data-stu-id="315a9-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="315a9-144">Zelfstudies over virtuele Windows-machines</span><span class="sxs-lookup"><span data-stu-id="315a9-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
