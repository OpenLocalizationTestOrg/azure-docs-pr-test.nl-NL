---
title: aaaDeploy licht op een virtuele Linux-machine Hello Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo licht stack is op een Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="aa1d6-103">LICHT stack Hello Azure CLI 1.0 implementeren</span><span class="sxs-lookup"><span data-stu-id="aa1d6-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="aa1d6-104">In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) in Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="aa1d6-105">U moet een Azure-Account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en Hallo [Azure CLI](../../cli-install-nodejs.md) die [tooyour Azure-account verbonden](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="aa1d6-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="aa1d6-106">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="aa1d6-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="aa1d6-107">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="aa1d6-108">[Azure CLI 1.0] – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="aa1d6-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="aa1d6-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="aa1d6-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="aa1d6-110">LICHT op bestaande virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="aa1d6-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="aa1d6-111">LICHT implementeren op nieuwe VM-overzicht</span><span class="sxs-lookup"><span data-stu-id="aa1d6-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="aa1d6-112">U kunt starten door het maken van een [resourcegroep](../../azure-resource-manager/resource-group-overview.md) waarin Hallo van nieuwe virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="aa1d6-113">toocreate Hallo VM zelf, kunt u een al geschreven Azure Resource Manager-sjabloon gevonden [hier op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="aa1d6-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="aa1d6-114">U ziet een antwoord sommige meer invoerwaarden vragen:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="aa1d6-115">U hebt nu een Linux-VM gemaakt met licht al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="aa1d6-116">Als u wenst, kunt u Hallo installatie controleren door te gaan naar beneden[controleren licht geïnstalleerd](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="aa1d6-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="aa1d6-117">LICHT implementeren op een bestaande VM-overzicht</span><span class="sxs-lookup"><span data-stu-id="aa1d6-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="aa1d6-118">Als u informatie over het maken van een Linux-VM nodig hebt, kunt u head [toolearn hier hoe toocreate een Linux-VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa1d6-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="aa1d6-119">Vervolgens moet u tooSSH in Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="aa1d6-120">Als u hulp nodig bij het maken van een SSH-sleutel, kunt u head [toolearn hier hoe toocreate een SSH-sleutel op Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa1d6-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="aa1d6-121">Als u een SSH-sleutel al hebt, gaat u verder gaan en SSH vanaf de opdrachtregel in uw Linux-VM met `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="aa1d6-122">Nu dat u binnen uw Linux-VM werkt, doorlopen we kunt Hallo licht stack installeren op op basis van Debian-distributies.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="aa1d6-123">Hallo exacte opdrachten kunnen afwijken voor andere Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="aa1d6-124">Installeren op Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="aa1d6-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="aa1d6-125">U moet hello-pakketten die worden geïnstalleerd na: `apache2`, `mysql-server`, `php5`, en `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="aa1d6-126">U kunt deze pakketten door rechtstreeks grabbing deze pakketten of met behulp van Tasksel installeren.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="aa1d6-127">Hieronder vindt u instructies voor beide opties.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="aa1d6-128">Voordat u installeert moet toodownload en lijsten pakket bijwerken.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="aa1d6-129">Afzonderlijke pakketten</span><span class="sxs-lookup"><span data-stu-id="aa1d6-129">Individual packages</span></span>
<span data-ttu-id="aa1d6-130">Met de apt get:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="aa1d6-131">Met behulp van tasksel</span><span class="sxs-lookup"><span data-stu-id="aa1d6-131">Using tasksel</span></span>
<span data-ttu-id="aa1d6-132">U kunt ook downloaden Tasksel, een hulpprogramma Debian/Ubuntu waarmee meerdere verwante pakketten worden geïnstalleerd als een gecoördineerde 'taak' op het systeem.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="aa1d6-133">Na het uitvoeren van een van de vorige opties hello, wordt u na vragen aan gebruiker tooinstall worden deze pakketten en verschillende andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="aa1d6-134">Druk op 'y' en klik vervolgens op 'Enter' toocontinue en volg alle andere tooset wordt u gevraagd een beheerderswachtwoord voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="aa1d6-135">Hiermee installeert u Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="aa1d6-136">Voer Hallo opdracht toosee volgen andere PHP-uitbreidingen die beschikbaar als pakketten zijn:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="aa1d6-137">Info.php document maken</span><span class="sxs-lookup"><span data-stu-id="aa1d6-137">Create info.php document</span></span>
<span data-ttu-id="aa1d6-138">Nu moet u kunnen toocheck welke versie van Apache, MySQL en PHP u via de opdrachtregel Hallo hebt typen `apache2 -v`, `mysql -v`, of `php -v`.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="aa1d6-139">Als u zou zoals tootest verder, maakt u een snelle PHP info pagina tooview in een browser.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="aa1d6-140">Maak een bestand met Nano teksteditor met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="aa1d6-141">Binnen Hallo GNU Nano teksteditor toevoegen Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="aa1d6-142">Vervolgens opslaan en sluiten Hallo teksteditor.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="aa1d6-143">Starten met deze opdracht Apache zodat alle nieuwe installaties van kracht.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="aa1d6-144">Controleer of licht is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="aa1d6-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="aa1d6-145">U kunt nu Hallo PHP pagina die u hebt gemaakt met een browser openen en zullen toohttp://youruniqueDNS/info.php controleren.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="aa1d6-146">Dit ziet vergelijkbare toothis afbeelding.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="aa1d6-147">U kunt de Apache-installatie controleren door Hallo Apache2 Ubuntu standaardpagina door te gaan tooyou http://youruniqueDNS/ weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="aa1d6-148">U ziet er ongeveer zo deze installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="aa1d6-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="aa1d6-149">Gefeliciteerd, u hebt alleen setup een licht-stack in uw Azure VM!</span><span class="sxs-lookup"><span data-stu-id="aa1d6-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa1d6-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa1d6-150">Next steps</span></span>
<span data-ttu-id="aa1d6-151">Bekijk Hallo Ubuntu-documentatie op Hallo licht stack:</span><span class="sxs-lookup"><span data-stu-id="aa1d6-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="aa1d6-152">https://Help.Ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="aa1d6-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png