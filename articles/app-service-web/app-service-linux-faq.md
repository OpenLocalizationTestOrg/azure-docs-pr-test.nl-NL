---
title: Web-App op Linux Veelgestelde vragen over Azure App Service | Microsoft Docs
description: Op Linux Veelgestelde vragen over Azure App Service Web-App.
keywords: Azure app service, web-app, veelgestelde vragen over, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="69bfb-104">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="69bfb-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="69bfb-105">Met het uitbrengen van Web-App op Linux, momenteel niets over het toevoegen van functies en er verbeteringen aangebracht in ons platform.</span><span class="sxs-lookup"><span data-stu-id="69bfb-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="69bfb-106">Hier volgen enkele veelgestelde vragen (FAQ) die onze klanten is aangevraagd door ons in de afgelopen maanden.</span><span class="sxs-lookup"><span data-stu-id="69bfb-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="69bfb-107">Als u een vraag, opmerking bij het artikel hebt en we deze zo snel mogelijk moet beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="69bfb-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="69bfb-108">Ingebouwde afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="69bfb-108">Built-in images</span></span>

<span data-ttu-id="69bfb-109">**V:** ik wil de ingebouwde Docker-containers die het platform biedt vertakken.</span><span class="sxs-lookup"><span data-stu-id="69bfb-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="69bfb-110">Waar vind ik die bestanden</span><span class="sxs-lookup"><span data-stu-id="69bfb-110">Where can I find those files?</span></span>

<span data-ttu-id="69bfb-111">**A:** vindt u alle Docker-bestanden op [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="69bfb-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="69bfb-112">U vindt alle Docker-containers op [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="69bfb-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="69bfb-113">**V:** wat zijn de verwachte waarden voor het starten van bestand sectie bij het configureren van de runtime-stack?</span><span class="sxs-lookup"><span data-stu-id="69bfb-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="69bfb-114">**A:** voor Node.Js, geeft u het configuratiebestand PM2 of het scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="69bfb-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="69bfb-115">Geef de naam van uw gecompileerde DLL voor .NET Core.</span><span class="sxs-lookup"><span data-stu-id="69bfb-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="69bfb-116">Voor Ruby, kunt u het Ruby script dat u wilt uw app met initialiseren.</span><span class="sxs-lookup"><span data-stu-id="69bfb-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="69bfb-117">Beheer</span><span class="sxs-lookup"><span data-stu-id="69bfb-117">Management</span></span>

<span data-ttu-id="69bfb-118">**V:** wat gebeurt er wanneer ik de schakelaar opnieuw opstarten in de Azure portal?</span><span class="sxs-lookup"><span data-stu-id="69bfb-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="69bfb-119">**A:** dit is het equivalent van Docker opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="69bfb-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="69bfb-120">**V:** kan ik Secure Shell (SSH) om verbinding met de app-container virtuele machine (VM) te gebruiken?</span><span class="sxs-lookup"><span data-stu-id="69bfb-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="69bfb-121">**A:** Ja, kunt u dat doen via de site SCM, Controleer het volgende artikel voor meer informatie [SSH-ondersteuning voor Web-App op Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="69bfb-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="69bfb-122">**V:** maken van een Linux-App Service-vlak via SDK of een ARM-sjabloon, hoe kan ik dit bereikt?</span><span class="sxs-lookup"><span data-stu-id="69bfb-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="69bfb-123">**A:** moet u de `reserved` veld van de app-service naar `true`.</span><span class="sxs-lookup"><span data-stu-id="69bfb-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="69bfb-124">Continue integratie/implementatie</span><span class="sxs-lookup"><span data-stu-id="69bfb-124">Continuous integration/deployment</span></span>

<span data-ttu-id="69bfb-125">**V:** mijn web-app nog steeds de installatiekopie van een oude Docker-container wordt gebruikt nadat ik de afbeelding op Docker-Hub hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="69bfb-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="69bfb-126">Continue integratie/implementatie van aangepaste containers ondersteund?</span><span class="sxs-lookup"><span data-stu-id="69bfb-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="69bfb-127">**A:** continue integratie/implementatie instellen voor Azure Container register of DockerHub door het controleren van het volgende artikel afbeeldingen [continue implementatie met de Azure-Web-App op Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="69bfb-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="69bfb-128">U kunt de container voor persoonlijke registers vernieuwen door te stoppen en vervolgens uw web-app te starten.</span><span class="sxs-lookup"><span data-stu-id="69bfb-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="69bfb-129">Of u kunt wijzigen of toevoegen van een dummy toepassingsinstelling geforceerd vernieuwen van de container.</span><span class="sxs-lookup"><span data-stu-id="69bfb-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="69bfb-130">**V:** ondersteunen testomgevingen?</span><span class="sxs-lookup"><span data-stu-id="69bfb-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="69bfb-131">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="69bfb-131">**A:** Yes.</span></span>

<span data-ttu-id="69bfb-132">**V:** kan ik gebruiken **webimplementatie** mijn web-app implementeren?</span><span class="sxs-lookup"><span data-stu-id="69bfb-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="69bfb-133">**A:** Ja, moet u een app instelling instellen `WEBSITE_WEBDEPLOY_USE_SCM` naar `false`.</span><span class="sxs-lookup"><span data-stu-id="69bfb-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="69bfb-134">Taalondersteuning</span><span class="sxs-lookup"><span data-stu-id="69bfb-134">Language support</span></span>

<span data-ttu-id="69bfb-135">**V:** bieden u ondersteuning voor niet-gecompileerde .NET Core apps?</span><span class="sxs-lookup"><span data-stu-id="69bfb-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="69bfb-136">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="69bfb-136">**A:** Yes.</span></span>

<span data-ttu-id="69bfb-137">**V:** u ondersteunen Composer als een afhankelijkheid manager voor PHP-apps?</span><span class="sxs-lookup"><span data-stu-id="69bfb-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="69bfb-138">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="69bfb-138">**A:** Yes.</span></span> <span data-ttu-id="69bfb-139">Tijdens een Git-implementatie moet Kudu detecteren die u een PHP-toepassing (dankzij de aanwezigheid van een composer.json-bestand implementeert) en een installatie composer geactiveerd voor u.</span><span class="sxs-lookup"><span data-stu-id="69bfb-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="69bfb-140">Aangepaste containers</span><span class="sxs-lookup"><span data-stu-id="69bfb-140">Custom containers</span></span>

<span data-ttu-id="69bfb-141">**V:** ik mijn eigen aangepaste container gebruik.</span><span class="sxs-lookup"><span data-stu-id="69bfb-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="69bfb-142">Mijn app bevindt zich in de `\home\` directory, maar ik kan mijn bestanden vinden wanneer ik de inhoud met behulp van bladeren de [SCM site](https://github.com/projectkudu/kudu) of een FTP-client.</span><span class="sxs-lookup"><span data-stu-id="69bfb-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="69bfb-143">Waar bevinden zich mijn bestanden?</span><span class="sxs-lookup"><span data-stu-id="69bfb-143">Where are my files?</span></span>

<span data-ttu-id="69bfb-144">**A:** We een SMB-share te koppelen van de `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="69bfb-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="69bfb-145">Hierdoor wordt de inhoud die is er overschreven.</span><span class="sxs-lookup"><span data-stu-id="69bfb-145">This will override any content that's there.</span></span>

<span data-ttu-id="69bfb-146">**V:** ik mijn eigen aangepaste container gebruik.</span><span class="sxs-lookup"><span data-stu-id="69bfb-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="69bfb-147">Ik wil niet dat het platform voor het koppelen van een SMB-share op de `\home\`.</span><span class="sxs-lookup"><span data-stu-id="69bfb-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="69bfb-148">**A:** kunt u dat doen door in te stellen de `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app-instelling op `false`.</span><span class="sxs-lookup"><span data-stu-id="69bfb-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="69bfb-149">**V:** Mijn aangepaste container lang duurt om te starten en de container van het platform opnieuw opstarten voordat is gestart.</span><span class="sxs-lookup"><span data-stu-id="69bfb-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="69bfb-150">**A:** kunt u de tijd die het platform wachten moet alvorens het opnieuw starten van de container.</span><span class="sxs-lookup"><span data-stu-id="69bfb-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="69bfb-151">Dit kan worden gedaan door het instellen van de `WEBSITES_CONTAINER_START_TIME_LIMIT` app-instelling op de gewenste waarde in seconden.</span><span class="sxs-lookup"><span data-stu-id="69bfb-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="69bfb-152">De standaardwaarde is 230 seconden en de maximale waarde is 600 seconden.</span><span class="sxs-lookup"><span data-stu-id="69bfb-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="69bfb-153">**V:** wat is de indeling voor de url van de server persoonlijke register?</span><span class="sxs-lookup"><span data-stu-id="69bfb-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="69bfb-154">**A:** moet u het volledige register url, zoals `http://` of `https://`.</span><span class="sxs-lookup"><span data-stu-id="69bfb-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="69bfb-155">**V:** wat is de indeling voor de naam van de installatiekopie in persoonlijke register optie?</span><span class="sxs-lookup"><span data-stu-id="69bfb-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="69bfb-156">**A:** moet u de naam van de volledige installatiekopie (bv de url van de persoonlijke register inclusief toevoegen.</span><span class="sxs-lookup"><span data-stu-id="69bfb-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="69bfb-157">myacr.azurecr.IO/DotNet:Latest)</span><span class="sxs-lookup"><span data-stu-id="69bfb-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="69bfb-158">**V:** ik wil meer dan één poort op de installatiekopie van mijn aangepaste container.</span><span class="sxs-lookup"><span data-stu-id="69bfb-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="69bfb-159">Is dit mogelijk?</span><span class="sxs-lookup"><span data-stu-id="69bfb-159">Is that possible?</span></span>

<span data-ttu-id="69bfb-160">**A:** momenteel, die niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="69bfb-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="69bfb-161">**V:** kan ik mijn eigen opslag brengen?</span><span class="sxs-lookup"><span data-stu-id="69bfb-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="69bfb-162">**A:** momenteel die niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="69bfb-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="69bfb-163">**V:** ik kan mijn aangepaste container bestand system of actief processen van de site SCM niet doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="69bfb-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="69bfb-164">Waarom is dat?</span><span class="sxs-lookup"><span data-stu-id="69bfb-164">Why is that?</span></span>

<span data-ttu-id="69bfb-165">**A:** de SCM-site wordt uitgevoerd in een afzonderlijke container.</span><span class="sxs-lookup"><span data-stu-id="69bfb-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="69bfb-166">U kunt het bestand systeem of met de processen van de app-container niet controleren.</span><span class="sxs-lookup"><span data-stu-id="69bfb-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="69bfb-167">**V:** Mijn aangepaste container luistert naar een andere poort dan poort 80.</span><span class="sxs-lookup"><span data-stu-id="69bfb-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="69bfb-168">Hoe kan ik mijn app voor het routeren van de aanvragen naar deze poort configureren?</span><span class="sxs-lookup"><span data-stu-id="69bfb-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="69bfb-169">**A:** hebben We automatische poortdetectie, ook kunt u een toepassing instelling opgeven **WEBSITES_PORT**, en wijs hieraan de waarde van het verwachte poortnummer.</span><span class="sxs-lookup"><span data-stu-id="69bfb-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="69bfb-170">Eerder het platform werd gebruikt `PORT` app instelt, we van plan bent deze app instellen voor het gebruik afschaffen en voor het gebruik van verplaatsen `WEBSITES_PORT` uitsluitend.</span><span class="sxs-lookup"><span data-stu-id="69bfb-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="69bfb-171">**V:** heb ik nodig voor het implementeren van HTTPS in Mijn aangepaste container.</span><span class="sxs-lookup"><span data-stu-id="69bfb-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="69bfb-172">**A:** Nee, het platform HTTPS-beëindiging aan de gedeelde frontends verwerkt.</span><span class="sxs-lookup"><span data-stu-id="69bfb-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="69bfb-173">Prijzen en SLA</span><span class="sxs-lookup"><span data-stu-id="69bfb-173">Pricing and SLA</span></span>

<span data-ttu-id="69bfb-174">**V:** wat is de prijzen terwijl u de openbare preview?</span><span class="sxs-lookup"><span data-stu-id="69bfb-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="69bfb-175">**A:** u kosten in rekening gebracht Halveer het aantal uren dat uw app wordt uitgevoerd, met de normale prijzen voor Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="69bfb-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="69bfb-176">Dit betekent dat u een korting van 50 procent op normale prijzen van Azure App Service krijgt.</span><span class="sxs-lookup"><span data-stu-id="69bfb-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="69bfb-177">Overige</span><span class="sxs-lookup"><span data-stu-id="69bfb-177">Other</span></span>

<span data-ttu-id="69bfb-178">**V:** wat zijn de ondersteunde tekens in toepassingsnamen instellingen?</span><span class="sxs-lookup"><span data-stu-id="69bfb-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="69bfb-179">**A:** u kunt alleen A-Z, a-z, 0-9 en het onderstrepingsteken gebruiken voor toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="69bfb-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="69bfb-180">**V:** waar kan ik nieuwe functies aanvragen?</span><span class="sxs-lookup"><span data-stu-id="69bfb-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="69bfb-181">**A:** dient u uw idee op de [forum met feedback van Web-Apps](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="69bfb-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="69bfb-182">'[Linux]' toevoegen aan de titel van uw idee.</span><span class="sxs-lookup"><span data-stu-id="69bfb-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69bfb-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69bfb-183">Next steps</span></span>
* [<span data-ttu-id="69bfb-184">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="69bfb-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="69bfb-185">SSH-ondersteuning voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="69bfb-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="69bfb-186">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="69bfb-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="69bfb-187">Continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="69bfb-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
