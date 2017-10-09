---
title: aaaDeploy licht op een virtuele Linux-machine in Azure | Microsoft Docs
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="f5bb2-103">LICHT stack in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="f5bb2-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="f5bb2-104">In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="f5bb2-105">U moet een Azure-account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en Hallo [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="f5bb2-106">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="f5bb2-107">Overzicht van de snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="f5bb2-107">Quick command summary</span></span>

1. <span data-ttu-id="f5bb2-108">Opslaan en bewerken van Hallo [azuredeploy.parameters.json bestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour voorkeur op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="f5bb2-109">Voer Hallo volgende twee opdrachten toocreate een resourcegroep en vervolgens de sjabloon te implementeren:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="f5bb2-110">LICHT op bestaande virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="f5bb2-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="f5bb2-111">Hallo volgende opdrachten updates pakketten vervolgens Apache, MySQL en PHP is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="f5bb2-112">LICHT implementeren op nieuwe VM-overzicht</span><span class="sxs-lookup"><span data-stu-id="f5bb2-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="f5bb2-113">Maak een resourcegroep met [az groep maken](/cli/azure/group#create) toocontain Hallo nieuwe virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="f5bb2-114">toocreate Hallo VM zelf, kunt u een al geschreven Azure Resource Manager-sjabloon gevonden [hier op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="f5bb2-115">Hallo opslaan [azuredeploy.parameters.json bestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="f5bb2-116">Hallo bewerken **azuredeploy.parameters.json** bestand tooyour voorkeur invoer.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="f5bb2-117">Hallo-sjabloon met implementeren [az implementatie maken] json-bestand verwijst naar Hallo gedownload:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="f5bb2-118">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-118">hello output is similar toohello following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="f5bb2-119">U hebt nu een Linux-VM gemaakt met licht al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="f5bb2-120">Als u wenst, kunt u Hallo installatie controleren door te gaan naar beneden[controleren licht geïnstalleerd](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="f5bb2-121">LICHT implementeren op een bestaande VM-overzicht</span><span class="sxs-lookup"><span data-stu-id="f5bb2-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="f5bb2-122">Als u informatie over het maken van een Linux-VM nodig hebt, kunt u head [toolearn hier hoe toocreate een Linux-VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="f5bb2-123">Vervolgens moet u tooSSH in Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="f5bb2-124">Als u hulp nodig bij het maken van een SSH-sleutel, kunt u head [toolearn hier hoe toocreate een SSH-sleutel op Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5bb2-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="f5bb2-125">Als u een SSH-sleutel al hebt, gaat u verder gaan en SSH vanaf de opdrachtregel in uw Linux-VM met `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="f5bb2-126">Nu dat u binnen uw Linux-VM werkt, doorlopen we kunt Hallo licht stack installeren op op basis van Debian-distributies.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="f5bb2-127">Hallo exacte opdrachten kunnen afwijken voor andere Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="f5bb2-128">Installeren op Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f5bb2-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="f5bb2-129">U moet hello-pakketten die worden geïnstalleerd na: `apache2`, `mysql-server`, `php5`, en `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="f5bb2-130">U kunt deze pakketten door rechtstreeks grabbing deze pakketten of met behulp van Tasksel installeren.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="f5bb2-131">Voordat u installeert moet toodownload en lijsten pakket bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="f5bb2-132">Afzonderlijke pakketten</span><span class="sxs-lookup"><span data-stu-id="f5bb2-132">Individual packages</span></span>
<span data-ttu-id="f5bb2-133">Met de apt get:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="f5bb2-134">Met behulp van tasksel</span><span class="sxs-lookup"><span data-stu-id="f5bb2-134">Using tasksel</span></span>
<span data-ttu-id="f5bb2-135">U kunt ook downloaden Tasksel, een hulpprogramma Debian/Ubuntu waarmee meerdere verwante pakketten worden geïnstalleerd als een gecoördineerde 'taak' op het systeem.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="f5bb2-136">Na het uitvoeren van een van de vorige opties hello, wordt u na vragen aan gebruiker tooinstall worden deze pakketten en verschillende andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="f5bb2-137">tooset een beheerderswachtwoord voor MySQL, druk op 'y' en klik vervolgens op 'Enter' toocontinue en volg alle andere aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="f5bb2-138">Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="f5bb2-139">Voer Hallo opdracht toosee volgen andere PHP-uitbreidingen die beschikbaar als pakketten zijn:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="f5bb2-140">Info.php document maken</span><span class="sxs-lookup"><span data-stu-id="f5bb2-140">Create info.php document</span></span>
<span data-ttu-id="f5bb2-141">Nu moet u kunnen toocheck welke versie van Apache, MySQL en PHP u via de opdrachtregel Hallo hebt typen `apache2 -v`, `mysql -v`, of `php -v`.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="f5bb2-142">Als u zou zoals tootest verder, maakt u een snelle PHP info pagina tooview in een browser.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="f5bb2-143">Maak een bestand met Nano teksteditor met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="f5bb2-144">Binnen Hallo GNU Nano teksteditor toevoegen Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="f5bb2-145">Vervolgens opslaan en sluiten Hallo teksteditor.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="f5bb2-146">Starten met deze opdracht Apache zodat alle nieuwe installaties van kracht.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="f5bb2-147">Controleer of licht is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="f5bb2-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="f5bb2-148">U kunt nu Hallo PHP pagina die u hebt gemaakt met een browser openen en zullen toohttp://youruniqueDNS/info.php controleren.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="f5bb2-149">Dit ziet vergelijkbare toothis afbeelding.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="f5bb2-150">U kunt de Apache-installatie controleren door Hallo Apache2 Ubuntu standaardpagina door te gaan tooyou http://youruniqueDNS/ weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f5bb2-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="f5bb2-151">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="f5bb2-152">Gefeliciteerd, u hebt alleen setup een licht-stack in uw Azure VM!</span><span class="sxs-lookup"><span data-stu-id="f5bb2-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5bb2-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5bb2-153">Next steps</span></span>
<span data-ttu-id="f5bb2-154">Bekijk Hallo Ubuntu-documentatie op Hallo licht stack:</span><span class="sxs-lookup"><span data-stu-id="f5bb2-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="f5bb2-155">https://Help.Ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="f5bb2-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
