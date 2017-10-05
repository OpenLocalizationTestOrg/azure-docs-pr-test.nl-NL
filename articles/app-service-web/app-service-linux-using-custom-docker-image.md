---
title: Het gebruik van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux | Microsoft Docs
description: Klik hier voor meer informatie over het gebruik van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux.
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
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="3de65-104">Met behulp van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="3de65-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="3de65-105">App Service biedt vooraf gedefinieerde toepassing stacks op Linux met ondersteuning voor specifieke versies, zoals PHP 7.0 en Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="3de65-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="3de65-106">Docker-containers op Linux-App Service gebruikt voor het hosten van deze vooraf gemaakte toepassing stacks.</span><span class="sxs-lookup"><span data-stu-id="3de65-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="3de65-107">U kunt ook een aangepaste Docker-installatiekopie gebruiken voor het implementeren van uw web-app naar de stack van een toepassing die niet al is gedefinieerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="3de65-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="3de65-108">Aangepaste Docker-installatiekopieën kunnen worden gehost op ofwel een openbaar of particulier Docker-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3de65-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="3de65-109">Procedure: een aangepaste Docker-installatiekopie voor een web-app instellen</span><span class="sxs-lookup"><span data-stu-id="3de65-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="3de65-110">U kunt de aangepaste Docker-afbeelding voor beide apps nieuwe en bestaande webs instellen.</span><span class="sxs-lookup"><span data-stu-id="3de65-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="3de65-111">Wanneer u een web-app maken in Linux in de [Azure-portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), klikt u op **configureren container** in te stellen van een aangepaste Docker-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="3de65-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Aangepaste Docker-installatiekopie voor een nieuwe WebApp op Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="3de65-113">Procedure: een aangepaste installatiekopie van Docker van Docker-Hub gebruiken</span><span class="sxs-lookup"><span data-stu-id="3de65-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="3de65-114">Gebruik een aangepaste installatiekopie Docker van Docker-Hub:</span><span class="sxs-lookup"><span data-stu-id="3de65-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="3de65-115">In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="3de65-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="3de65-116">Selecteer **Docker Hub** als de **Afbeeldingsbron**, klik dan ofwel **openbare** of **persoonlijke** en typt u de **installatiekopie en optionele tagnaam**, zoals `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="3de65-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="3de65-117">De **startopdracht** is set automatisch op basis van wat is gedefinieerd in de Docker-bestand, maar u kunt uw eigen opdrachten instellen.</span><span class="sxs-lookup"><span data-stu-id="3de65-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Afbeelding van de openbare opslagplaats Docker Hub configureren][2]

    <span data-ttu-id="3de65-119">Wanneer uw installatiekopie van een persoonlijke bibliotheek is, moet u ook de referenties van de Docker-Hub als invoeren (**aanmelding gebruikersnaam** en **wachtwoord**) voor de opslagplaats voor persoonlijke Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="3de65-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Afbeelding van de opslagplaats voor persoonlijke Docker Hub configureren][3]

3. <span data-ttu-id="3de65-121">Nadat u de container hebt geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3de65-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="3de65-122">Het gebruik van een Docker-installatiekopie uit het register van een persoonlijke afbeelding</span><span class="sxs-lookup"><span data-stu-id="3de65-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="3de65-123">Een aangepaste Docker-installatiekopie uit het register van een persoonlijke installatiekopie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3de65-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="3de65-124">In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="3de65-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="3de65-125">Klik op **persoonlijke register** als de **Afbeeldingsbron**.</span><span class="sxs-lookup"><span data-stu-id="3de65-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="3de65-126">Voer de **installatiekopie en de optionele codenaam**, **Server-URL** voor het persoonlijke register, samen met de referenties (**aanmelding gebruikersnaam** en **wachtwoord**).</span><span class="sxs-lookup"><span data-stu-id="3de65-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="3de65-127">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3de65-127">Click **Save**.</span></span>

    ![Afbeelding van Docker uit persoonlijke register configureren][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="3de65-129">Hoe: Stel de poort die wordt gebruikt door de Docker-afbeelding</span><span class="sxs-lookup"><span data-stu-id="3de65-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="3de65-130">Wanneer u een aangepaste Docker-installatiekopie voor uw web-app gebruikt, kunt u de `WEBSITES_PORT` omgevingsvariabele in uw Dockerfile die wordt toegevoegd aan de gegenereerde container.</span><span class="sxs-lookup"><span data-stu-id="3de65-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="3de65-131">Houd rekening met het volgende voorbeeld van een docker-bestand voor een Ruby toepassing:</span><span class="sxs-lookup"><span data-stu-id="3de65-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="3de65-132">Op de laatste regel van de opdracht ziet u dat de omgevingsvariabele WEBSITES_PORT wordt doorgegeven tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="3de65-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="3de65-133">Houd er rekening mee dat hoofdlettergebruik van belang in opdrachten is.</span><span class="sxs-lookup"><span data-stu-id="3de65-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="3de65-134">Eerder het platform werd gebruikt `PORT` app instelt, we van plan bent deze app instellen voor het gebruik afschaffen en voor het gebruik van verplaatsen `WEBSITES_PORT` uitsluitend.</span><span class="sxs-lookup"><span data-stu-id="3de65-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="3de65-135">Wanneer u een bestaande Docker-installatiekopie gemaakt door iemand anders gebruikt, moet u mogelijk een andere poort dan poort 80 voor de toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="3de65-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="3de65-136">Voeg een toepassingsinstelling met de naam voor het configureren van de poort `WEBSITES_PORT` met de waarde zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3de65-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![App-poortinstelling voor de installatiekopie van een aangepaste Docker configureren][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="3de65-138">Procedure: de opstarttijd van uw installatiekopie Docker instellen</span><span class="sxs-lookup"><span data-stu-id="3de65-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="3de65-139">Standaard, als uw container niet wordt gestart voordat 230 seconden, opnieuw het platform de container.</span><span class="sxs-lookup"><span data-stu-id="3de65-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="3de65-140">Als uw aangepaste Docker-installatiekopie in meer dan 230 seconden wordt gestart, kunt u de `WEBSITES_CONTAINER_START_TIME_LIMIT` app instelt, de waarde voor deze instelling is in seconden, hierdoor kan de platform-Houd uw container uitgevoerd voordat u deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3de65-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="3de65-141">De standaardwaarde is 230 seconden en de maximale toegestane waarde is 600 seconden.</span><span class="sxs-lookup"><span data-stu-id="3de65-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="3de65-142">Hoe: ontkoppelen van de opgegeven platform-opslag</span><span class="sxs-lookup"><span data-stu-id="3de65-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="3de65-143">Standaard wordt het platform een permanente storage-share te koppelen van de `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="3de65-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="3de65-144">Als uw installatiekopie container niet nodig heeft voor een permanente share, kunt u uitschakelen dat opslag koppelen door in te stellen de `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app-instelling op `false`.</span><span class="sxs-lookup"><span data-stu-id="3de65-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="3de65-145">U hebt nog steeds toegang tot deze opslag van de site scm en alle Docker-Logboeken (indien ingeschakeld) worden geschreven naar de logboekbestanden die worden gegenereerd door het platform.</span><span class="sxs-lookup"><span data-stu-id="3de65-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="3de65-146">Hoe: Ga terug naar de met de installatiekopie van een ingebouwde</span><span class="sxs-lookup"><span data-stu-id="3de65-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="3de65-147">Overschakelen van met een aangepaste installatiekopie voor het gebruik van een installatiekopie van het ingebouwde:</span><span class="sxs-lookup"><span data-stu-id="3de65-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="3de65-148">In de [Azure-portal](https://portal.azure.com), vervolgens uw web-app op Linux, niet vinden in **instellingen** klikt u op **App Service**.</span><span class="sxs-lookup"><span data-stu-id="3de65-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="3de65-149">Selecteer uw **Runtime Stack** wilt gebruiken voor de installatiekopie van het ingebouwde, klikt u vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3de65-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Afbeelding van de ingebouwde Docker configureren][5]


## <a name="troubleshooting"></a><span data-ttu-id="3de65-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3de65-151">Troubleshooting</span></span> ##

<span data-ttu-id="3de65-152">Als uw toepassing om te beginnen met uw aangepaste Docker-installatiekopie is mislukt, Controleer u dat de Docker-Logboeken in de map met logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="3de65-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="3de65-153">U kunt toegang tot deze map via uw SCM-site of via de FTP.</span><span class="sxs-lookup"><span data-stu-id="3de65-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="3de65-154">Logboek de `stdout` en `stderr` van de container, moet u inschakelen **Docker-Container logboekregistratie** onder **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="3de65-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Logboekregistratie inschakelen][8]

![Met behulp van Kudu Docker-logboeken weergeven][7]

<span data-ttu-id="3de65-157">U toegang hebt tot de site SCM bij **geavanceerde hulpmiddelen** in de **ontwikkelingsprogramma's** menu.</span><span class="sxs-lookup"><span data-stu-id="3de65-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3de65-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3de65-158">Next Steps</span></span> ##

<span data-ttu-id="3de65-159">Volg de volgende koppelingen aan de slag met Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="3de65-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="3de65-160">Inleiding tot Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="3de65-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="3de65-161">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="3de65-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="3de65-162">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3de65-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="3de65-163">Post een bericht vragen en problemen op [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="3de65-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
