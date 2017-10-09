---
title: aaaDeploy LEMP op een virtuele Linux-machine in Azure | Microsoft Docs
description: Zelfstudie - installatie Hallo LEMP stack op een Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="49891-103">Een webserver LEMP installeren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="49891-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="49891-104">In dit artikel leert u hoe een NGINX toodeploy web server, MySQL en PHP (Hallo LEMP stack) op een Ubuntu VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="49891-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="49891-105">Hallo LEMP stack is een populaire alternatief toohello [licht stack](tutorial-lamp-stack.md), die u kunt ook installeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="49891-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="49891-106">toosee hello LEMP server in actie, kunt u optioneel installeren en configureren van een WordPress-site.</span><span class="sxs-lookup"><span data-stu-id="49891-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="49891-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="49891-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="49891-108">Maak een VM Ubuntu (hello "L" in hello LEMP-stack)</span><span class="sxs-lookup"><span data-stu-id="49891-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="49891-109">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="49891-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="49891-110">NGINX, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="49891-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="49891-111">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="49891-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="49891-112">WordPress op Hallo LEMP server installeren</span><span class="sxs-lookup"><span data-stu-id="49891-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49891-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="49891-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="49891-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="49891-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49891-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49891-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="49891-116">NGINX, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="49891-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="49891-117">Voer de volgende opdracht tooupdate Ubuntu pakket bronnen Hallo en NGINX, MySQL en PHP installeren.</span><span class="sxs-lookup"><span data-stu-id="49891-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="49891-118">U bent na vragen aan gebruiker tooinstall hello-pakketten en andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="49891-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="49891-119">Wanneer u wordt gevraagd, moet u een root-wachtwoord instellen voor MySQL en [Enter] toocontinue.</span><span class="sxs-lookup"><span data-stu-id="49891-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="49891-120">Ga als volgt Hallo resterende prompts.</span><span class="sxs-lookup"><span data-stu-id="49891-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="49891-121">Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL.</span><span class="sxs-lookup"><span data-stu-id="49891-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Pagina MySQL root-wachtwoord][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="49891-123">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="49891-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="49891-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="49891-124">NGINX</span></span>

<span data-ttu-id="49891-125">Hallo-versie van NGINX Hello opdracht volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="49891-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="49891-126">Met NGINX geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="49891-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="49891-127">tooview hello NGINX welkomstpagina, open een webbrowser en voer het openbare IP-adres Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="49891-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="49891-128">Gebruik Hallo openbaar IP-adres tooSSH toohello VM die wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="49891-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Standaard-NGINX-pagina][3]


### <a name="mysql"></a><span data-ttu-id="49891-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="49891-130">MySQL</span></span>

<span data-ttu-id="49891-131">Hallo-versie van MySQL controleren met de volgende opdracht Hallo (Houd er rekening mee Hallo kapitaal `V` parameter):</span><span class="sxs-lookup"><span data-stu-id="49891-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="49891-132">U wordt aangeraden Hallo na de installatie van script toohelp beveiligde Hallo van MySQL uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="49891-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="49891-133">Voer uw hoofdwachtwoord MySQL en Hallo beveiligingsinstellingen configureren voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="49891-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="49891-134">Als u toocreate een MySQL-database wilt, gebruikers toevoegen of wijzigen van configuratie-instellingen, aanmelding tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="49891-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="49891-135">Wanneer u klaar bent, sluit u Hallo mysql prompt door typen `\q`.</span><span class="sxs-lookup"><span data-stu-id="49891-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="49891-136">PHP</span><span class="sxs-lookup"><span data-stu-id="49891-136">PHP</span></span>

<span data-ttu-id="49891-137">Hallo-versie van PHP controleren met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="49891-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="49891-138">Configureer NGINX toouse Hallo PHP FastCGI-proces Manager (PHP-Rambus).</span><span class="sxs-lookup"><span data-stu-id="49891-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="49891-139">Voer Hallo opdrachten tooback Hallo oorspronkelijke NGINX-Server-configuratiebestand blokkeren en bewerk vervolgens Hallo oorspronkelijke bestand in een editor naar keuze te volgen:</span><span class="sxs-lookup"><span data-stu-id="49891-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="49891-140">In de editor Hallo Hallo inhoud van vervangen `/etc/nginx/sites-available/default` door Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="49891-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="49891-141">Hallo-opmerkingen voor uitleg van Hallo instellingen bekijken.</span><span class="sxs-lookup"><span data-stu-id="49891-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="49891-142">Vervang Hallo openbare IP-adres van uw virtuele machine voor *yourPublicIPAddress*, en laat Hallo resterende instellingen.</span><span class="sxs-lookup"><span data-stu-id="49891-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="49891-143">Sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="49891-143">Then save hello file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="49891-144">Controleer de configuratie van de Hallo NGINX syntaxisfouten:</span><span class="sxs-lookup"><span data-stu-id="49891-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="49891-145">Als Hallo syntaxis juist is, opnieuw opstarten NGINX Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="49891-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="49891-146">Als u meer tootest wilt, maakt u een snelle PHP info pagina tooview in een browser.</span><span class="sxs-lookup"><span data-stu-id="49891-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="49891-147">Hallo volgende opdracht maakt Hallo PHP pagina:</span><span class="sxs-lookup"><span data-stu-id="49891-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="49891-148">U kunt nu controleren Hallo PHP info-pagina die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49891-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="49891-149">Open een browser en ga te`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="49891-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="49891-150">Vervang Hallo openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49891-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="49891-151">Dit ziet vergelijkbare toothis afbeelding.</span><span class="sxs-lookup"><span data-stu-id="49891-151">It should look similar toothis image.</span></span>

![Pagina voor PHP-info][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="49891-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49891-153">Next steps</span></span>

<span data-ttu-id="49891-154">In deze zelfstudie maakt u een server LEMP in Azure geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="49891-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="49891-155">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="49891-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="49891-156">Een virtuele Ubuntu-machine maken</span><span class="sxs-lookup"><span data-stu-id="49891-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="49891-157">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="49891-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="49891-158">NGINX, MySQL en PHP installeren</span><span class="sxs-lookup"><span data-stu-id="49891-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="49891-159">Controleer of de installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="49891-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="49891-160">WordPress installeren op Hallo LEMP stack</span><span class="sxs-lookup"><span data-stu-id="49891-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="49891-161">Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="49891-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49891-162">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="49891-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
