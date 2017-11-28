---
title: Quick Start - aaaAzure maken VM CLI | Microsoft Docs
description: Snel meer toocreate virtuele machines met hello Azure CLI.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="7e24c-103">Een virtuele Linux-machine maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7e24c-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="7e24c-104">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="7e24c-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="7e24c-105">Deze handleiding details hello Azure CLI toodeploy met een virtuele machine met Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="7e24c-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="7e24c-106">Zodra Hallo-server is geïmplementeerd, een SSH-verbinding wordt gemaakt en een NGINX-webserver is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7e24c-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="7e24c-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="7e24c-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7e24c-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="7e24c-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7e24c-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="7e24c-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7e24c-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7e24c-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="7e24c-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7e24c-111">Create a resource group</span></span>

<span data-ttu-id="7e24c-112">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e24c-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7e24c-113">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="7e24c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7e24c-114">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="7e24c-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7e24c-115">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="7e24c-115">Create virtual machine</span></span>

<span data-ttu-id="7e24c-116">Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e24c-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="7e24c-117">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* en SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="7e24c-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="7e24c-118">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="7e24c-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="7e24c-119">Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="7e24c-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="7e24c-120">Let op Hallo `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="7e24c-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="7e24c-121">Dit adres is gebruikte tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7e24c-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="7e24c-122">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="7e24c-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="7e24c-123">Standaard worden alleen SSH-verbindingen toegestaan naar virtuele Linux-machines die zijn geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7e24c-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="7e24c-124">Als deze virtuele machine wordt toobe een webserver, moet u tooopen poort 80 van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="7e24c-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="7e24c-125">Gebruik Hallo [az vm open poort](/cli/azure/vm#open-port) opdracht tooopen Hallo gewenst poort.</span><span class="sxs-lookup"><span data-stu-id="7e24c-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="7e24c-126">SSH in uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7e24c-126">SSH into your VM</span></span>

<span data-ttu-id="7e24c-127">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7e24c-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="7e24c-128">Zorg ervoor dat tooreplace  *<publicIpAddress>*  Hello Corrigeer openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7e24c-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="7e24c-129">In ons voorbeeld hierboven was *40.68.254.142* ons IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7e24c-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="7e24c-130">NGINX installeren</span><span class="sxs-lookup"><span data-stu-id="7e24c-130">Install NGINX</span></span>

<span data-ttu-id="7e24c-131">Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e24c-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="7e24c-132">Hallo-NGINX welkomstpagina weergeven</span><span class="sxs-lookup"><span data-stu-id="7e24c-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="7e24c-133">U kunt een webbrowser van uw keuze tooview hello NGINX standaardwelkomstpagina gebruiken van NGINX geïnstalleerd en de poort 80 is nu open op de virtuele machine van de Internet - Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e24c-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="7e24c-134">Ervoor toouse Hallo worden *publicIpAddress* u hiervoor toovisit Hallo standaardpagina beschreven.</span><span class="sxs-lookup"><span data-stu-id="7e24c-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="7e24c-136">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="7e24c-136">Clean up resources</span></span>

<span data-ttu-id="7e24c-137">Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="7e24c-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7e24c-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e24c-138">Next steps</span></span>

<span data-ttu-id="7e24c-139">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7e24c-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="7e24c-140">toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7e24c-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="7e24c-141">Zelfstudies over virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="7e24c-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
