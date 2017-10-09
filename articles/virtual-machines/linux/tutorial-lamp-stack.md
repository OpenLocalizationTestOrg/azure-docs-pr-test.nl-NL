---
title: aaaDeploy licht op een virtuele Linux-machine in Azure | Microsoft Docs
description: Zelfstudie - installatie Hallo licht stack op een Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="5cb37-103">Een webserver licht installeren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="5cb37-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="5cb37-104">In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) op een Ubuntu VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb37-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="5cb37-105">Als u liever Hallo NGINX-webserver, Zie Hallo [LEMP stack](tutorial-lemp-stack.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5cb37-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="5cb37-106">toosee hello licht server in actie, kunt u optioneel installeren en configureren van een WordPress-site.</span><span class="sxs-lookup"><span data-stu-id="5cb37-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="5cb37-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="5cb37-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5cb37-108">Maak een VM Ubuntu (hello "L" in hello licht-stack)</span><span class="sxs-lookup"><span data-stu-id="5cb37-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="5cb37-109">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="5cb37-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="5cb37-110">Apache, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="5cb37-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="5cb37-111">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="5cb37-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="5cb37-112">WordPress op Hallo licht server installeren</span><span class="sxs-lookup"><span data-stu-id="5cb37-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="5cb37-113">Zie voor meer informatie over Hallo licht stack, met inbegrip van aanbevelingen voor een productieomgeving Hallo [Ubuntu documentatie](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="5cb37-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5cb37-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="5cb37-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5cb37-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="5cb37-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5cb37-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5cb37-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="5cb37-117">Apache, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="5cb37-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="5cb37-118">Voer de volgende opdracht tooupdate Ubuntu pakket bronnen Hallo en Apache, MySQL en PHP installeren.</span><span class="sxs-lookup"><span data-stu-id="5cb37-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="5cb37-119">Houd er rekening mee Hallo dakje (^) aan Hallo einde van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="5cb37-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="5cb37-120">U bent na vragen aan gebruiker tooinstall hello-pakketten en andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5cb37-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="5cb37-121">Wanneer u wordt gevraagd, moet u een root-wachtwoord instellen voor MySQL en [Enter] toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5cb37-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="5cb37-122">Ga als volgt Hallo resterende prompts.</span><span class="sxs-lookup"><span data-stu-id="5cb37-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="5cb37-123">Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cb37-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Pagina MySQL root-wachtwoord][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="5cb37-125">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="5cb37-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="5cb37-126">Apache</span><span class="sxs-lookup"><span data-stu-id="5cb37-126">Apache</span></span>

<span data-ttu-id="5cb37-127">Hallo-versie van Apache Hello opdracht volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="5cb37-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="5cb37-128">Met Apache geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="5cb37-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="5cb37-129">tooview hello Apache2 Ubuntu standaardpagina, open een webbrowser en voer het openbare IP-adres Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="5cb37-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="5cb37-130">Gebruik Hallo openbaar IP-adres tooSSH toohello VM die wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5cb37-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Apache standaardpagina][3]


### <a name="mysql"></a><span data-ttu-id="5cb37-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="5cb37-132">MySQL</span></span>

<span data-ttu-id="5cb37-133">Hallo-versie van MySQL controleren met de volgende opdracht Hallo (Houd er rekening mee Hallo kapitaal `V` parameter):</span><span class="sxs-lookup"><span data-stu-id="5cb37-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="5cb37-134">U wordt aangeraden Hallo na de installatie van script toohelp beveiligde Hallo van MySQL uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="5cb37-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="5cb37-135">Voer uw hoofdwachtwoord MySQL en Hallo beveiligingsinstellingen configureren voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5cb37-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="5cb37-136">Als u toocreate een MySQL-database wilt, gebruikers toevoegen of wijzigen van configuratie-instellingen, aanmelding tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="5cb37-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="5cb37-137">Wanneer u klaar bent, sluit u Hallo mysql prompt door typen `\q`.</span><span class="sxs-lookup"><span data-stu-id="5cb37-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="5cb37-138">PHP</span><span class="sxs-lookup"><span data-stu-id="5cb37-138">PHP</span></span>

<span data-ttu-id="5cb37-139">Hallo-versie van PHP controleren met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5cb37-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="5cb37-140">Als u meer tootest wilt, maakt u een snelle PHP info pagina tooview in een browser.</span><span class="sxs-lookup"><span data-stu-id="5cb37-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="5cb37-141">Hallo volgende opdracht maakt Hallo PHP pagina:</span><span class="sxs-lookup"><span data-stu-id="5cb37-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="5cb37-142">U kunt nu controleren Hallo PHP info-pagina die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5cb37-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="5cb37-143">Open een browser en ga te`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="5cb37-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="5cb37-144">Vervang Hallo openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5cb37-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="5cb37-145">Dit ziet vergelijkbare toothis afbeelding.</span><span class="sxs-lookup"><span data-stu-id="5cb37-145">It should look similar toothis image.</span></span>

![Pagina voor PHP-info][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="5cb37-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5cb37-147">Next steps</span></span>

<span data-ttu-id="5cb37-148">In deze zelfstudie maakt u een server licht in Azure geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5cb37-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="5cb37-149">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="5cb37-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5cb37-150">Een virtuele Ubuntu-machine maken</span><span class="sxs-lookup"><span data-stu-id="5cb37-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="5cb37-151">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="5cb37-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="5cb37-152">Apache, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="5cb37-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="5cb37-153">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="5cb37-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="5cb37-154">WordPress op Hallo licht server installeren</span><span class="sxs-lookup"><span data-stu-id="5cb37-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="5cb37-155">Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="5cb37-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5cb37-156">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="5cb37-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png