---
title: Quick Start - aaaAzure maken Windows VM CLI | Microsoft Docs
description: Meer toocreate snel een virtuele machines van Windows Hello Azure CLI.
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
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="f152a-103">Maken van een virtuele machine van Windows Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f152a-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="f152a-104">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="f152a-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="f152a-105">Deze handleiding details hello Azure CLI toodeploy met een virtuele machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f152a-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="f152a-106">Zodra de implementatie is voltooid, we toohello server verbinden en IIS installeren.</span><span class="sxs-lookup"><span data-stu-id="f152a-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="f152a-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="f152a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f152a-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="f152a-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f152a-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="f152a-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f152a-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f152a-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="f152a-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f152a-111">Create a resource group</span></span>

<span data-ttu-id="f152a-112">Maak een resourcegroep maken met [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f152a-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f152a-113">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="f152a-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f152a-114">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="f152a-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="f152a-115">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="f152a-115">Create virtual machine</span></span>

<span data-ttu-id="f152a-116">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f152a-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="f152a-117">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f152a-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="f152a-118">In dit voorbeeld wordt *azureuser* voor de naam van een gebruiker met beheerdersrechten en *myPassword12* Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f152a-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="f152a-119">Deze waarden toosomething juiste tooyour omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f152a-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="f152a-120">Deze waarden nodig wanneer u een verbinding met de Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f152a-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="f152a-121">Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="f152a-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="f152a-122">Let op Hallo `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="f152a-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="f152a-123">Dit adres is gebruikte tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f152a-123">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="f152a-124">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="f152a-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="f152a-125">Standaard worden alleen de RDP-verbindingen zijn toegestaan in tooWindows virtuele machines zijn geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f152a-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="f152a-126">Als deze virtuele machine wordt toobe een webserver, moet u tooopen poort 80 van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="f152a-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="f152a-127">Gebruik Hallo [az vm open poort](/cli/azure/vm#open-port) opdracht tooopen Hallo gewenst poort.</span><span class="sxs-lookup"><span data-stu-id="f152a-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="f152a-128">Verbinding maken met toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="f152a-128">Connect toovirtual machine</span></span>

<span data-ttu-id="f152a-129">Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f152a-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="f152a-130">Hallo IP-adres vervangen door Hallo openbaar IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f152a-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="f152a-131">Wanneer u wordt gevraagd, voert u Hallo-referenties gebruikt bij het maken van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f152a-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="f152a-132">IIS installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f152a-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="f152a-133">Nu dat u hebt geregistreerd in Azure VM toohello, kunt u één regel PowerShell tooinstall IIS gebruiken en Hallo lokale firewall regel tooallow-webverkeer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f152a-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="f152a-134">Open een PowerShell-prompt en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f152a-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="f152a-135">Weergave Hallo IIS-welkomstpagina</span><span class="sxs-lookup"><span data-stu-id="f152a-135">View hello IIS welcome page</span></span>

<span data-ttu-id="f152a-136">Met IIS is geïnstalleerd en poort 80 is nu open op de virtuele machine uit Hallo Internet, kunt u een webbrowser van uw keuze tooview Hallo IIS standaardwelkomstpagina.</span><span class="sxs-lookup"><span data-stu-id="f152a-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="f152a-137">Worden ervoor toouse Hallo openbaar IP-adres die u hiervoor toovisit Hallo standaardpagina beschreven.</span><span class="sxs-lookup"><span data-stu-id="f152a-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="f152a-139">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="f152a-139">Clean up resources</span></span>

<span data-ttu-id="f152a-140">Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="f152a-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f152a-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f152a-141">Next steps</span></span>

<span data-ttu-id="f152a-142">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f152a-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="f152a-143">toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="f152a-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f152a-144">Zelfstudies over virtuele Windows-machines</span><span class="sxs-lookup"><span data-stu-id="f152a-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
