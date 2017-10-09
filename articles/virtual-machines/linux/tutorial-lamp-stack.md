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
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Een webserver licht installeren op een virtuele machine in Azure
In dit artikel leert u hoe toodeploy een Apache web server, MySQL en PHP (Hallo licht stack) op een Ubuntu VM in Azure. Als u liever Hallo NGINX-webserver, Zie Hallo [LEMP stack](tutorial-lemp-stack.md) zelfstudie. toosee hello licht server in actie, kunt u optioneel installeren en configureren van een WordPress-site. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een VM Ubuntu (hello "L" in hello licht-stack)
> * Poort 80 openen voor webverkeer
> * Apache, MySQL en PHP installeren
> * Controleer of de installatie en configuratie
> * WordPress op Hallo licht server installeren


Zie voor meer informatie over Hallo licht stack, met inbegrip van aanbevelingen voor een productieomgeving Hallo [Ubuntu documentatie](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Apache, MySQL en PHP installeren

Voer de volgende opdracht tooupdate Ubuntu pakket bronnen Hallo en Apache, MySQL en PHP installeren. Houd er rekening mee Hallo dakje (^) aan Hallo einde van Hallo-opdracht.


```bash
sudo apt update && sudo apt install lamp-server^
```



U bent na vragen aan gebruiker tooinstall hello-pakketten en andere afhankelijkheden. Wanneer u wordt gevraagd, moet u een root-wachtwoord instellen voor MySQL en [Enter] toocontinue. Ga als volgt Hallo resterende prompts. Dit proces installeert Hallo minimale vereiste PHP-uitbreidingen nodig toouse PHP met MySQL. 

![Pagina MySQL root-wachtwoord][1]

## <a name="verify-installation-and-configuration"></a>Controleer of de installatie en configuratie


### <a name="apache"></a>Apache

Hallo-versie van Apache Hello opdracht volgende controleren:
```bash
apache2 -v
```

Met Apache geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet. tooview hello Apache2 Ubuntu standaardpagina, open een webbrowser en voer het openbare IP-adres Hallo Hallo VM. Gebruik Hallo openbaar IP-adres tooSSH toohello VM die wordt gebruikt:

![Apache standaardpagina][3]


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

Als u meer tootest wilt, maakt u een snelle PHP info pagina tooview in een browser. Hallo volgende opdracht maakt Hallo PHP pagina:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

U kunt nu controleren Hallo PHP info-pagina die u hebt gemaakt. Open een browser en ga te`http://yourPublicIPAddress/info.php`. Vervang Hallo openbare IP-adres van uw virtuele machine. Dit ziet vergelijkbare toothis afbeelding.

![Pagina voor PHP-info][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een server licht in Azure geïmplementeerd. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een virtuele Ubuntu-machine maken
> * Poort 80 openen voor webverkeer
> * Apache, MySQL en PHP installeren
> * Controleer of de installatie en configuratie
> * WordPress op Hallo licht server installeren

Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.

> [!div class="nextstepaction"]
> [Webserver met SSL beveiligde](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png