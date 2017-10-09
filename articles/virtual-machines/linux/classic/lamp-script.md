---
title: aaaUse Hallo extensie CustomScript op een Linux-VM | Microsoft Docs
description: Meer informatie over hoe toouse hello CustomScript extensie toodeploy toepassingen op Linux virtuele Machines in Azure gemaakt met het klassieke implementatiemodel Hallo.
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
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="d9389-103">Een licht-app met behulp van de extensie CustomScript Azure Hallo voor Linux implementeren</span><span class="sxs-lookup"><span data-stu-id="d9389-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d9389-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d9389-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d9389-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d9389-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d9389-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9389-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d9389-107">Zie voor meer informatie over het implementeren van een licht stack Hallo Resource Manager-model met [hier](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9389-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d9389-108">Hallo CustomScript uitbreiding voor Microsoft Azure voor Linux biedt een manier toocustomize uw virtuele machines (VM's) door het uitvoeren van willekeurige code geschreven in een scripttaal die wordt ondersteund door Hallo VM (bijvoorbeeld, Python en Bash).</span><span class="sxs-lookup"><span data-stu-id="d9389-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="d9389-109">Dit biedt een zeer flexibele manier tooautomate toepassing implementatie toomultiple machines.</span><span class="sxs-lookup"><span data-stu-id="d9389-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="d9389-110">U kunt de extensie CustomScript Hallo implementeren met behulp van hello Azure-portal, Windows PowerShell of hello Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d9389-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="d9389-111">In dit artikel we gebruiken hello Azure CLI toodeploy een eenvoudige licht toepassing tooan Ubuntu VM gemaakt met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9389-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9389-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9389-112">Prerequisites</span></span>
<span data-ttu-id="d9389-113">In dit voorbeeld maakt u eerst twee virtuele Azure-machines met Ubuntu 14.04 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d9389-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="d9389-114">Hallo VMs heten *script vm* en *licht vm*.</span><span class="sxs-lookup"><span data-stu-id="d9389-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="d9389-115">Unieke namen gebruiken bij het maken van virtuele machines Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9389-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="d9389-116">Een gebruikte toorun Hallo CLI-opdrachten is en één gebruikte toodeploy Hallo licht app.</span><span class="sxs-lookup"><span data-stu-id="d9389-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="d9389-117">U moet ook een Azure Storage-account en een sleutel tooaccess it (u kunt dit krijgen via hello Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="d9389-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="d9389-118">Als u informatie over het maken van virtuele Linux-machines in Azure nodig te verwijzen[maken van een virtuele Machine waarop Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="d9389-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="d9389-119">Hallo installeren opdrachten wordt ervan uitgegaan dat Ubuntu, maar u kunt Hallo installatie aanpassen voor een Linux-distro ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d9389-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="d9389-120">Hallo moet script vm VM toohave die Azure CLI hebt geïnstalleerd, met een werkende verbinding tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d9389-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="d9389-121">Voor hulp bij dit te verwijzen[installeren en configureren van hello Azure-opdrachtregelinterface](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9389-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="d9389-122">Uploaden van een script</span><span class="sxs-lookup"><span data-stu-id="d9389-122">Upload a script</span></span>
<span data-ttu-id="d9389-123">We gebruiken Hallo extensie CustomScript toorun een script op een externe VM tooinstall Hallo licht stack en maken van een PHP-pagina.</span><span class="sxs-lookup"><span data-stu-id="d9389-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="d9389-124">In de volgorde tooaccess Hallo script vanaf elke locatie hebt we het uploaden als een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="d9389-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="d9389-125">Script-overzicht</span><span class="sxs-lookup"><span data-stu-id="d9389-125">Script overview</span></span>
<span data-ttu-id="d9389-126">Voorbeeld van een script Hallo een licht stack tooUbuntu (inclusief het instellen van een stille installatie van MySQL) installeert, schrijft u een eenvoudige PHP-bestand en Apache wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d9389-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="d9389-127">Script uploaden</span><span class="sxs-lookup"><span data-stu-id="d9389-127">Upload script</span></span>
<span data-ttu-id="d9389-128">Sla Hallo script op als een tekstbestand, bijvoorbeeld *install_lamp.sh*, en upload het tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="d9389-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="d9389-129">U kunt dit eenvoudig doen met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d9389-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="d9389-130">Hallo volgende voorbeeld wordt geüpload Hallo bestand tooa storage-container met de naam 'scripts'.</span><span class="sxs-lookup"><span data-stu-id="d9389-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="d9389-131">Als het Hallo-container bestaat niet moet u toocreate het eerste.</span><span class="sxs-lookup"><span data-stu-id="d9389-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="d9389-132">Maak ook een JSON-bestand dat wordt beschreven hoe toodownload Hallo script uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d9389-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="d9389-133">Opslaan als *public_config.json* ('mystorage' met de naam van uw opslagaccount Hallo vervangen):</span><span class="sxs-lookup"><span data-stu-id="d9389-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="d9389-134">Hallo-extensie implementeren</span><span class="sxs-lookup"><span data-stu-id="d9389-134">Deploy hello extension</span></span>
<span data-ttu-id="d9389-135">Nu kunt u Hallo volgende opdracht toodeploy Hallo de extensie CustomScript Linux toohello externe virtuele machine met behulp van Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9389-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="d9389-136">vorige opdracht Hallo gedownload en uitgevoerd Hallo *install_lamp.sh* script op Hallo VM aangeroepen *licht vm*.</span><span class="sxs-lookup"><span data-stu-id="d9389-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="d9389-137">Aangezien Hallo app een webserver bevat, onthouden tooopen een HTTP-luisterpoort op Hallo met de volgende opdracht Hallo externe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d9389-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="d9389-138">Bewaking en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="d9389-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="d9389-139">U kunt controleren hoe goed Hallo aangepast script wordt uitgevoerd door te kijken Hallo logboekbestand op Hallo extern VM.</span><span class="sxs-lookup"><span data-stu-id="d9389-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="d9389-140">SSH te*licht vm* en tail Hallo-logboekbestand met de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9389-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="d9389-141">Nadat u de extensie CustomScript Hallo hebt uitgevoerd, kunt u bladeren toohello PHP pagina die u hebt gemaakt voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9389-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="d9389-142">Hallo PHP pagina Hallo bijvoorbeeld in dit artikel is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="d9389-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9389-143">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d9389-143">Additional resources</span></span>
<span data-ttu-id="d9389-144">U kunt dezelfde basisstappen toodeploy Hallo complexere apps.</span><span class="sxs-lookup"><span data-stu-id="d9389-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="d9389-145">In dit voorbeeld is het installatiescript Hallo opgeslagen als een openbare blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d9389-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="d9389-146">Een veiligere optie toostore Hallo installatiescript zou zijn als een beveiligde blob met een [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="d9389-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="d9389-147">Aanvullende bronnen voor Azure CLI-, Linux- en de extensie CustomScript Hallo worden naast weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9389-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="d9389-148">Voor het automatiseren van taken voor het virtuele Linux-machine aanpassen met behulp van de extensie CustomScript</span><span class="sxs-lookup"><span data-stu-id="d9389-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="d9389-149">Azure Linux-extensies (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d9389-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)