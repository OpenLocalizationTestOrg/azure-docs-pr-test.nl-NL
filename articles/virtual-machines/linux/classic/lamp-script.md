---
title: De extensie CustomScript gebruiken op een virtuele Linux-machine | Microsoft Docs
description: Informatie over het gebruik van de extensie CustomScript voor het implementeren van toepassingen op Linux virtuele Machines in Azure gemaakt met behulp van het klassieke implementatiemodel.
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="deb04-103">Een LAMP-app implementeren met de Azure CustomScript-extensie voor Linux</span><span class="sxs-lookup"><span data-stu-id="deb04-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="deb04-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="deb04-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="deb04-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="deb04-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="deb04-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="deb04-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="deb04-107">Zie voor meer informatie over het implementeren van een licht stack met het Resource Manager-model [hier](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="deb04-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="deb04-108">De Microsoft Azure CustomScript-extensie voor Linux biedt een manier voor het aanpassen van uw virtuele machines (VM's) door het uitvoeren van willekeurige code geschreven in een scripttaal die wordt ondersteund door de virtuele machine (bijvoorbeeld, Python en Bash).</span><span class="sxs-lookup"><span data-stu-id="deb04-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="deb04-109">Dit biedt een zeer flexibele manier voor het automatiseren van de toepassingsimplementatie op meerdere machines.</span><span class="sxs-lookup"><span data-stu-id="deb04-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="deb04-110">U kunt de extensie CustomScript met de Azure portal, Windows PowerShell of de Azure-opdrachtregelinterface (Azure CLI) implementeren.</span><span class="sxs-lookup"><span data-stu-id="deb04-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="deb04-111">In dit artikel we gebruiken de Azure CLI voor het implementeren van een eenvoudige toepassing licht voor een VM Ubuntu gemaakt met het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="deb04-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deb04-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="deb04-112">Prerequisites</span></span>
<span data-ttu-id="deb04-113">In dit voorbeeld maakt u eerst twee virtuele Azure-machines met Ubuntu 14.04 of hoger.</span><span class="sxs-lookup"><span data-stu-id="deb04-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="deb04-114">De virtuele machines worden genoemd *script vm* en *licht vm*.</span><span class="sxs-lookup"><span data-stu-id="deb04-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="deb04-115">Unieke namen gebruiken bij het maken van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="deb04-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="deb04-116">Een de CLI-opdrachten uitvoeren wordt gebruikt en een wordt gebruikt om de app licht te implementeren.</span><span class="sxs-lookup"><span data-stu-id="deb04-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="deb04-117">U moet ook een Azure Storage-account en een sleutel voor toegang tot deze (u kunt dit opvragen bij de Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="deb04-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="deb04-118">Als u informatie over het maken van virtuele Linux-machines in Azure moet verwijzen naar [maken van een virtuele Machine waarop Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="deb04-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="deb04-119">De installatie-opdrachten wordt ervan uitgegaan Ubuntu, maar u kunt de installatie voor alle ondersteunde Linux-distro aanpassen.</span><span class="sxs-lookup"><span data-stu-id="deb04-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="deb04-120">De script-vm-virtuele machine moet beschikken over de Azure CLI hebt geïnstalleerd, met een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="deb04-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="deb04-121">Voor hulp bij dit naar verwijzen [installeren en configureren van de Azure-opdrachtregelinterface](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="deb04-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="deb04-122">Uploaden van een script</span><span class="sxs-lookup"><span data-stu-id="deb04-122">Upload a script</span></span>
<span data-ttu-id="deb04-123">De extensie CustomScript gebruiken we een script uitvoeren op een externe virtuele machine voor het installeren van de stack licht en maken van een PHP-pagina.</span><span class="sxs-lookup"><span data-stu-id="deb04-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="deb04-124">Om het script vanaf elke locatie toegang te krijgen moet we het uploaden als een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="deb04-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="deb04-125">Script-overzicht</span><span class="sxs-lookup"><span data-stu-id="deb04-125">Script overview</span></span>
<span data-ttu-id="deb04-126">Voorbeeld van het script een licht-stack in Ubuntu (inclusief het instellen van een stille installatie van MySQL) geïnstalleerd, schrijft u een eenvoudige PHP-bestand en Apache wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="deb04-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="deb04-127">Script uploaden</span><span class="sxs-lookup"><span data-stu-id="deb04-127">Upload script</span></span>
<span data-ttu-id="deb04-128">Sla het script als een tekstbestand, bijvoorbeeld *install_lamp.sh*, en vervolgens te uploaden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="deb04-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="deb04-129">U kunt dit eenvoudig doen met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="deb04-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="deb04-130">Het volgende voorbeeld wordt het bestand naar een storage-container met de naam 'scripts' geüpload.</span><span class="sxs-lookup"><span data-stu-id="deb04-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="deb04-131">Als de container bestaat niet moet u deze eerst maken.</span><span class="sxs-lookup"><span data-stu-id="deb04-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="deb04-132">Maak ook een JSON-bestand dat wordt beschreven hoe u het script downloaden van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="deb04-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="deb04-133">Opslaan als *public_config.json* ('mystorage' met de naam van uw opslagaccount vervangen):</span><span class="sxs-lookup"><span data-stu-id="deb04-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="deb04-134">De extensie implementeren</span><span class="sxs-lookup"><span data-stu-id="deb04-134">Deploy the extension</span></span>
<span data-ttu-id="deb04-135">U kunt nu de volgende opdracht gebruiken voor het implementeren van de Linux-extensie CustomScript op de externe virtuele machine met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="deb04-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="deb04-136">De vorige opdracht worden gedownload en wordt uitgevoerd de *install_lamp.sh* script op de virtuele machine aangeroepen *licht vm*.</span><span class="sxs-lookup"><span data-stu-id="deb04-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="deb04-137">Omdat de app een webserver bevat, moet u een HTTP-luisterpoort op de externe virtuele machine openen met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="deb04-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="deb04-138">Bewaking en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="deb04-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="deb04-139">U kunt controleren hoe goed het aangepaste script door te kijken naar het logboekbestand op de externe virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="deb04-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="deb04-140">SSH kunt uitvoeren naar *licht vm* en staart van het logboekbestand met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="deb04-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="deb04-141">Nadat u de extensie CustomScript hebt uitgevoerd, kunt u bladeren naar de PHP-pagina die u hebt gemaakt voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="deb04-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="deb04-142">De PHP-pagina voor het voorbeeld in dit artikel is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="deb04-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="deb04-143">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="deb04-143">Additional resources</span></span>
<span data-ttu-id="deb04-144">U kunt dezelfde basisstappen om complexere apps te implementeren.</span><span class="sxs-lookup"><span data-stu-id="deb04-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="deb04-145">In dit voorbeeld is het installatiescript opgeslagen als een openbare blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="deb04-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="deb04-146">Een veiligere optie zijn voor het opslaan van het script voor installatie als een beveiligde blob met een [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="deb04-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="deb04-147">Aanvullende bronnen voor Azure CLI-, Linux- en de extensie CustomScript worden naast weergegeven.</span><span class="sxs-lookup"><span data-stu-id="deb04-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="deb04-148">Voor het automatiseren van taken voor het virtuele Linux-machine aanpassen met behulp van de extensie CustomScript</span><span class="sxs-lookup"><span data-stu-id="deb04-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="deb04-149">Azure Linux-extensies (GitHub)</span><span class="sxs-lookup"><span data-stu-id="deb04-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)