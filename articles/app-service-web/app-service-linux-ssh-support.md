---
title: ondersteuning voor Azure App Service Web-App op Linux aaaSSH | Microsoft Docs
description: Meer informatie over het gebruik van SSH met Azure-Web-App op Linux.
keywords: Azure app service, web-app, linux, oss
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a>SSH-ondersteuning voor Azure-Web-App op Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Overzicht

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is een cryptografische netwerkprotocol voor het gebruik van netwerkservices veilig. Het is meest gebruikte toolog in een systeem op afstand veilig vanaf een opdrachtregel en administratieve opdrachten extern uit te voeren.

Web-App op Linux biedt SSH-ondersteuning in app-container Hallo met elk Hallo ingebouwde Docker-afbeeldingen die worden gebruikt voor Hallo Runtime-Stack van nieuwe web-apps. 

![Runtime-Stacks](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

U kunt ook SSH gebruiken met aangepaste installatiekopieën Docker door waaronder Hallo SSH-server als onderdeel van de installatiekopie van het Hallo en deze te configureren zoals beschreven in dit onderwerp.



## <a name="making-a-client-connection"></a>Maken van een clientverbinding

toomake hello primaire site van een SSH-clientverbinding moet worden gestart. 

Plak Hallo Source Control Management (SCM) eindpunt voor uw web-app in uw browser met Hallo formulier te volgen:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Als u zijn niet geverifieerd, bent u vereiste tooauthenticate met uw Azure-abonnement tooconnect.

![SSH-verbinding](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Ondersteuning van SSH met aangepaste Docker-installatiekopieën

Uitvoeren om een aangepaste Docker installatiekopie toosupport SSH-communicatie tussen Hallo-container en Hallo-client in hello Azure-portal, Hallo volgende stappen uit voor uw Docker-installatiekopie. 

Deze stappen zijn worden weergegeven in hello Azure App Service-opslagplaats als voorbeeld [hier](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Hallo omvatten `openssh-server` installatie in [ `RUN` instructie](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile voor uw installatiekopie en het Hallo wachtwoord voor het hoofdaccount hello te`"Docker!"`. 

    > [!NOTE] 
    > Deze configuratie is niet toegestaan voor externe verbindingen toohello container. SSH kan alleen worden benaderd via Hallo Kudu / SCM-Site, die is geverifieerd met behulp van Hallo publishing referenties.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Voeg een [ `COPY` instructie](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy een [sshd_config](http://man.openbsd.org/sshd_config) bestand toohello */enzovoort/ssh/* directory. Het configuratiebestand moet worden gebaseerd op onze sshd_config-bestand in Azure App Service-GitHub-opslagplaats voor Hallo [hier](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Hallo *sshd_config* bestand moet de volgende Hallo bevatten of Hallo verbinding is mislukt: 
    > * `Ciphers`moet ten minste een van de volgende Hallo opnemen: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`moet ten minste een van de volgende Hallo opnemen: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Poort 2222 opnemen in Hallo [ `EXPOSE` instructie](https://docs.docker.com/engine/reference/builder/#expose) voor Hallo Dockerfile. Hoewel het hoofdwachtwoord Hallo bekend is, poort 2222 niet toegankelijk vanuit Hallo internet. Het is een interne alleen poort toegankelijk alleen door containers in Hallo Brugnetwerk van een virtueel particulier netwerk.

    ```docker
    EXPOSE 2222 80
    ```

4. Zorg ervoor dat toostart Hallo ssh-service. Hallo voorbeeld [hier](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) maakt gebruik van een shellscript in */bin* directory.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Hallo Dockerfile gebruikt Hallo [ `CMD` instructie](https://docs.docker.com/engine/reference/builder/#cmd) toorun Hallo script.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Volgende stappen
Zie Hallo volgende koppelingen voor meer informatie over Web-App op Linux. U kunt vragen en problemen op boeken [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux](app-service-linux-using-custom-docker-image.md)
* [Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux](app-service-linux-using-nodejs-pm2.md)
* [Met behulp van .NET Core in Azure-Web-App op Linux](app-service-linux-using-dotnetcore.md)
* [Met behulp van Ruby in Azure-Web-App op Linux](app-service-linux-ruby-get-started.md)
* [Web-App op Linux Veelgestelde vragen over Azure App Service](app-service-linux-faq.md)

