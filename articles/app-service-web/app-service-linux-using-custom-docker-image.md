---
title: aaaHow toouse een aangepaste Docker-afbeelding voor Azure-Web-App op Linux | Microsoft Docs
description: Hoe een aangepaste Docker toouse afbeelding voor Azure-Web-App op Linux.
keywords: Azure app service, web-app, linux, docker, container
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="ecb35-104">Met behulp van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ecb35-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="ecb35-105">App Service biedt vooraf gedefinieerde toepassing stacks op Linux met ondersteuning voor specifieke versies, zoals PHP 7.0 en Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="ecb35-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="ecb35-106">Op Linux-App Service gebruikt Docker-containers toohost deze kan toepassing stacks vooraf gebouwd.</span><span class="sxs-lookup"><span data-stu-id="ecb35-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="ecb35-107">U kunt een aangepaste installatiekopie toodeploy voor Docker ook uw web-app tooan toepassing stack die niet al is gedefinieerd in Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ecb35-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="ecb35-108">Aangepaste Docker-installatiekopieën kunnen worden gehost op ofwel een openbaar of particulier Docker-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ecb35-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="ecb35-109">Procedure: een aangepaste Docker-installatiekopie voor een web-app instellen</span><span class="sxs-lookup"><span data-stu-id="ecb35-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="ecb35-110">U kunt aangepaste Docker-installatiekopie Hallo voor zowel nieuwe en bestaande webs apps instellen.</span><span class="sxs-lookup"><span data-stu-id="ecb35-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="ecb35-111">Wanneer u een web-app maken in Linux in Hallo [Azure-portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), klikt u op **configureren container** tooset een aangepaste Docker-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="ecb35-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Aangepaste Docker-installatiekopie voor een nieuwe WebApp op Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="ecb35-113">Procedure: een aangepaste installatiekopie van Docker van Docker-Hub gebruiken</span><span class="sxs-lookup"><span data-stu-id="ecb35-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="ecb35-114">toouse een aangepaste installatiekopie Docker van Docker-Hub:</span><span class="sxs-lookup"><span data-stu-id="ecb35-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="ecb35-115">In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="ecb35-116">Selecteer **Docker Hub** als Hallo **Afbeeldingsbron**, klik dan ofwel **openbare** of **persoonlijke** en type Hallo **installatiekopie en optionele tagnaam**, zoals `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="ecb35-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="ecb35-117">Hallo **startopdracht** is set automatisch op basis van wat is gedefinieerd in Hallo Docker-bestand, maar u kunt uw eigen opdrachten instellen.</span><span class="sxs-lookup"><span data-stu-id="ecb35-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Afbeelding van de openbare opslagplaats Docker Hub configureren][2]

    <span data-ttu-id="ecb35-119">Wanneer uw installatiekopie van een persoonlijke bibliotheek is, moet u ook tooenter hello Docker Hub referenties als (**aanmelding gebruikersnaam** en **wachtwoord**) voor Hallo persoonlijke Docker-Hub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ecb35-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Afbeelding van de opslagplaats voor persoonlijke Docker Hub configureren][3]

3. <span data-ttu-id="ecb35-121">Nadat u de container Hallo hebt geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="ecb35-122">Hoe toouse een Docker een installatiekopie van een installatiekopie van het persoonlijke register</span><span class="sxs-lookup"><span data-stu-id="ecb35-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="ecb35-123">een aangepaste Docker-installatiekopie uit het register van een installatiekopie van persoonlijke toouse:</span><span class="sxs-lookup"><span data-stu-id="ecb35-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="ecb35-124">In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="ecb35-125">Klik op **persoonlijke register** als Hallo **Afbeeldingsbron**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="ecb35-126">Voer Hallo **installatiekopie en de optionele codenaam**, **Server-URL** voor persoonlijke register hello, samen met de Hallo referenties (**aanmelding gebruikersnaam** en **wachtwoord** ).</span><span class="sxs-lookup"><span data-stu-id="ecb35-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="ecb35-127">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-127">Click **Save**.</span></span>

    ![Afbeelding van Docker uit persoonlijke register configureren][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="ecb35-129">Hoe: Hallo-poort die wordt gebruikt door uw installatiekopie Docker instellen</span><span class="sxs-lookup"><span data-stu-id="ecb35-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="ecb35-130">Wanneer u een aangepaste Docker-installatiekopie voor uw web-app gebruikt, kunt u Hallo `WEBSITES_PORT` omgevingsvariabele in uw Dockerfile, toohello gegenereerd container wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ecb35-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="ecb35-131">Overweeg het volgende voorbeeld van een docker-bestand voor een Ruby toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="ecb35-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="ecb35-132">U ziet op de laatste regel van de opdracht Hallo dat die Hallo WEBSITES_PORT-omgevingsvariabele wordt doorgegeven tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ecb35-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="ecb35-133">Houd er rekening mee dat hoofdlettergebruik van belang in opdrachten is.</span><span class="sxs-lookup"><span data-stu-id="ecb35-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="ecb35-134">Eerder Hallo platform werd gebruikt `PORT` app instelt, we van plan bent toodeprecate Hallo Gebruik deze app instellen en verplaatsen toousing `WEBSITES_PORT` uitsluitend.</span><span class="sxs-lookup"><span data-stu-id="ecb35-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="ecb35-135">Wanneer u een bestaande Docker-installatiekopie gemaakt door iemand anders gebruikt, moet u mogelijk een andere poort dan poort 80 toospecify voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ecb35-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="ecb35-136">tooconfigure Hallo poort, het toevoegen van een benoemde toepassingsinstelling `WEBSITES_PORT` met Hallo waarde zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ecb35-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![App-poortinstelling voor de installatiekopie van een aangepaste Docker configureren][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="ecb35-138">Hoe: Hallo starten van de tijd voor uw installatiekopie Docker instellen</span><span class="sxs-lookup"><span data-stu-id="ecb35-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="ecb35-139">Standaard, als uw container niet wordt gestart voordat 230 seconden opnieuw Hallo platform de container.</span><span class="sxs-lookup"><span data-stu-id="ecb35-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="ecb35-140">Als uw aangepaste Docker-installatiekopie in meer dan 230 seconden wordt gestart, kunt u Hallo `WEBSITES_CONTAINER_START_TIME_LIMIT` instellen, app Hallo-waarde voor deze instelling is in seconden, wordt hierdoor Hallo platform behouden uw container uitgevoerd voordat u deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ecb35-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="ecb35-141">Hallo-standaardwaarde is 230 seconden en Hallo maximaal toegestane waarde is 600 seconden.</span><span class="sxs-lookup"><span data-stu-id="ecb35-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="ecb35-142">Hoe: ontkoppelen Hallo platform opgegeven opslag</span><span class="sxs-lookup"><span data-stu-id="ecb35-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="ecb35-143">Standaard gekoppeld Hallo platform een permanente opslag share toohello `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="ecb35-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="ecb35-144">Als uw installatiekopie container niet nodig heeft voor een permanente share, kunt u uitschakelen dat opslag koppelen door de instelling Hallo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app instellen te`false`.</span><span class="sxs-lookup"><span data-stu-id="ecb35-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="ecb35-145">U hebt nog altijd toegang tot toothat opslag van Hallo scm-site en alle Docker-Logboeken (indien ingeschakeld) toohello logboekbestanden gegenereerd door het Hallo-platform worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="ecb35-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="ecb35-146">Hoe: gaat u terug toousing een installatiekopie van het ingebouwde</span><span class="sxs-lookup"><span data-stu-id="ecb35-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="ecb35-147">tooswitch van het gebruik van een aangepaste installatiekopie toousing een ingebouwde installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="ecb35-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="ecb35-148">In Hallo [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **App Service**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="ecb35-149">Selecteer uw **Runtime Stack** toouse Hallo ingebouwde afbeelding, klikt u vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Afbeelding van de ingebouwde Docker configureren][5]


## <a name="troubleshooting"></a><span data-ttu-id="ecb35-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ecb35-151">Troubleshooting</span></span> ##

<span data-ttu-id="ecb35-152">Wanneer uw toepassing toostart door uw aangepaste Docker-installatiekopie mislukt, controleert u Hallo die docker Hallo logboekbestanden directory zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="ecb35-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="ecb35-153">U kunt toegang tot deze map via uw SCM-site of via de FTP.</span><span class="sxs-lookup"><span data-stu-id="ecb35-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="ecb35-154">Hallo toolog `stdout` en `stderr` van de container, moet u tooenable **Docker-Container logboekregistratie** onder **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="ecb35-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Logboekregistratie inschakelen][8]

![Met behulp van Kudu tooview Docker-Logboeken][7]

<span data-ttu-id="ecb35-157">U toegang hebt tot Hallo SCM site uit **geavanceerde hulpmiddelen** in Hallo **ontwikkelingsprogramma's** menu.</span><span class="sxs-lookup"><span data-stu-id="ecb35-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecb35-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ecb35-158">Next Steps</span></span> ##

<span data-ttu-id="ecb35-159">Ga als volgt Hallo volgen koppelingen tooget de slag met Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="ecb35-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="ecb35-160">Inleiding tooAzure Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ecb35-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="ecb35-161">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="ecb35-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="ecb35-162">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ecb35-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="ecb35-163">Post een bericht vragen en problemen op [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="ecb35-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
