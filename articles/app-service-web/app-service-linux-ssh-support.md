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
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="ca950-104">SSH-ondersteuning voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ca950-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="ca950-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ca950-105">Overview</span></span>

<span data-ttu-id="ca950-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is een cryptografische netwerkprotocol voor het gebruik van netwerkservices veilig.</span><span class="sxs-lookup"><span data-stu-id="ca950-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="ca950-107">Het is meest gebruikte toolog in een systeem op afstand veilig vanaf een opdrachtregel en administratieve opdrachten extern uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ca950-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="ca950-108">Web-App op Linux biedt SSH-ondersteuning in app-container Hallo met elk Hallo ingebouwde Docker-afbeeldingen die worden gebruikt voor Hallo Runtime-Stack van nieuwe web-apps.</span><span class="sxs-lookup"><span data-stu-id="ca950-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Runtime-Stacks](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="ca950-110">U kunt ook SSH gebruiken met aangepaste installatiekopieën Docker door waaronder Hallo SSH-server als onderdeel van de installatiekopie van het Hallo en deze te configureren zoals beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ca950-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="ca950-111">Maken van een clientverbinding</span><span class="sxs-lookup"><span data-stu-id="ca950-111">Making a client connection</span></span>

<span data-ttu-id="ca950-112">toomake hello primaire site van een SSH-clientverbinding moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="ca950-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="ca950-113">Plak Hallo Source Control Management (SCM) eindpunt voor uw web-app in uw browser met Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca950-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="ca950-114">Als u zijn niet geverifieerd, bent u vereiste tooauthenticate met uw Azure-abonnement tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ca950-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![SSH-verbinding](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="ca950-116">Ondersteuning van SSH met aangepaste Docker-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="ca950-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="ca950-117">Uitvoeren om een aangepaste Docker installatiekopie toosupport SSH-communicatie tussen Hallo-container en Hallo-client in hello Azure-portal, Hallo volgende stappen uit voor uw Docker-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="ca950-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="ca950-118">Deze stappen zijn worden weergegeven in hello Azure App Service-opslagplaats als voorbeeld [hier](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="ca950-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="ca950-119">Hallo omvatten `openssh-server` installatie in [ `RUN` instructie](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile voor uw installatiekopie en het Hallo wachtwoord voor het hoofdaccount hello te`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="ca950-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="ca950-120">Deze configuratie is niet toegestaan voor externe verbindingen toohello container.</span><span class="sxs-lookup"><span data-stu-id="ca950-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="ca950-121">SSH kan alleen worden benaderd via Hallo Kudu / SCM-Site, die is geverifieerd met behulp van Hallo publishing referenties.</span><span class="sxs-lookup"><span data-stu-id="ca950-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="ca950-122">Voeg een [ `COPY` instructie](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy een [sshd_config](http://man.openbsd.org/sshd_config) bestand toohello */enzovoort/ssh/* directory.</span><span class="sxs-lookup"><span data-stu-id="ca950-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="ca950-123">Het configuratiebestand moet worden gebaseerd op onze sshd_config-bestand in Azure App Service-GitHub-opslagplaats voor Hallo [hier](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="ca950-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca950-124">Hallo *sshd_config* bestand moet de volgende Hallo bevatten of Hallo verbinding is mislukt:</span><span class="sxs-lookup"><span data-stu-id="ca950-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="ca950-125">`Ciphers`moet ten minste een van de volgende Hallo opnemen: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="ca950-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="ca950-126">`MACs`moet ten minste een van de volgende Hallo opnemen: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="ca950-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="ca950-127">Poort 2222 opnemen in Hallo [ `EXPOSE` instructie](https://docs.docker.com/engine/reference/builder/#expose) voor Hallo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="ca950-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="ca950-128">Hoewel het hoofdwachtwoord Hallo bekend is, poort 2222 niet toegankelijk vanuit Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="ca950-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="ca950-129">Het is een interne alleen poort toegankelijk alleen door containers in Hallo Brugnetwerk van een virtueel particulier netwerk.</span><span class="sxs-lookup"><span data-stu-id="ca950-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="ca950-130">Zorg ervoor dat toostart Hallo ssh-service.</span><span class="sxs-lookup"><span data-stu-id="ca950-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="ca950-131">Hallo voorbeeld [hier](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) maakt gebruik van een shellscript in */bin* directory.</span><span class="sxs-lookup"><span data-stu-id="ca950-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="ca950-132">Hallo Dockerfile gebruikt Hallo [ `CMD` instructie](https://docs.docker.com/engine/reference/builder/#cmd) toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="ca950-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="ca950-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca950-133">Next steps</span></span>
<span data-ttu-id="ca950-134">Zie Hallo volgende koppelingen voor meer informatie over Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="ca950-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="ca950-135">U kunt vragen en problemen op boeken [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="ca950-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="ca950-136">Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ca950-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="ca950-137">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ca950-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="ca950-138">Met behulp van .NET Core in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ca950-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="ca950-139">Met behulp van Ruby in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ca950-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="ca950-140">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ca950-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

