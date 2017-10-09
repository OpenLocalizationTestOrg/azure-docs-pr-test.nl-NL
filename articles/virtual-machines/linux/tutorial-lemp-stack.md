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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Een webserver LEMP installeren op een virtuele machine in Azure
In dit artikel leert u hoe een NGINX toodeploy web server, MySQL en PHP (Hallo LEMP stack) op een Ubuntu VM in Azure. Hallo LEMP stack is een populaire alternatief toohello [licht stack](tutorial-lamp-stack.md), die u kunt ook installeren in Azure. toosee hello LEMP server in actie, kunt u optioneel installeren en configureren van een WordPress-site. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een VM Ubuntu (hello "L" in hello LEMP-stack)
> * Poort 80 openen voor webverkeer
> * NGINX, MySQL en PHP installeren
> * Controleer of de installatie en configuratie
> * WordPress op Hallo LEMP server installeren


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>NGINX, MySQL en PHP installeren

Voer de volgende opdracht tooupdate Ubuntu pakket bronnen Hallo en NGINX, MySQL en PHP installeren. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

U bent na vragen aan gebruiker tooinstall hello-pakketten en andere afhankelijkheden. Wanneer u wordt gevraagd, moet u een root-wachtwoord instellen voor MySQL en [Enter] toocontinue. Ga als volgt Hallo resterende prompts. Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL. 

![Pagina MySQL root-wachtwoord][1]

## <a name="verify-installation-and-configuration"></a>Controleer of de installatie en configuratie


### <a name="nginx"></a>NGINX

Hallo-versie van NGINX Hello opdracht volgende controleren:
```bash
nginx -v
```

Met NGINX geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet. tooview hello NGINX welkomstpagina, open een webbrowser en voer het openbare IP-adres Hallo Hallo VM. Gebruik Hallo openbaar IP-adres tooSSH toohello VM die wordt gebruikt:

![Standaard-NGINX-pagina][3]


### <a name="mysql"></a>MySQL

Hallo-versie van MySQL controleren met de volgende opdracht Hallo (Houd er rekening mee Hallo kapitaal `V` parameter):

```bash
msql -V
```

U wordt aangeraden Hallo na de installatie van script toohelp beveiligde Hallo van MySQL uitgevoerd:

```bash
mysql_secure_installation
```

Voer uw hoofdwachtwoord MySQL en Hallo beveiligingsinstellingen configureren voor uw omgeving.

Als u toocreate een MySQL-database wilt, gebruikers toevoegen of wijzigen van configuratie-instellingen, aanmelding tooMySQL:

```bash
mysql -u root -p
```

Wanneer u klaar bent, sluit u Hallo mysql prompt door typen `\q`.

### <a name="php"></a>PHP

Hallo-versie van PHP controleren met de volgende opdracht Hallo:

```bash
php -v
```

Configureer NGINX toouse Hallo PHP FastCGI-proces Manager (PHP-Rambus). Voer Hallo opdrachten tooback Hallo oorspronkelijke NGINX-Server-configuratiebestand blokkeren en bewerk vervolgens Hallo oorspronkelijke bestand in een editor naar keuze te volgen:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

In de editor Hallo Hallo inhoud van vervangen `/etc/nginx/sites-available/default` door Hallo volgende. Hallo-opmerkingen voor uitleg van Hallo instellingen bekijken. Vervang Hallo openbare IP-adres van uw virtuele machine voor *yourPublicIPAddress*, en laat Hallo resterende instellingen. Sla Hallo-bestand.

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

Controleer de configuratie van de Hallo NGINX syntaxisfouten:

```bash
sudo nginx -t
```

Als Hallo syntaxis juist is, opnieuw opstarten NGINX Hello volgende opdracht:

```bash
sudo service nginx restart
```

Als u meer tootest wilt, maakt u een snelle PHP info pagina tooview in een browser. Hallo volgende opdracht maakt Hallo PHP pagina:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



U kunt nu controleren Hallo PHP info-pagina die u hebt gemaakt. Open een browser en ga te`http://yourPublicIPAddress/info.php`. Vervang Hallo openbare IP-adres van uw virtuele machine. Dit ziet vergelijkbare toothis afbeelding.

![Pagina voor PHP-info][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een server LEMP in Azure geïmplementeerd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een virtuele Ubuntu-machine maken
> * Poort 80 openen voor webverkeer
> * NGINX, MySQL en PHP installeren
> * Controleer of de installatie en configuratie
> * WordPress installeren op Hallo LEMP stack

Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.

> [!div class="nextstepaction"]
> [Webserver met SSL beveiligde](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
