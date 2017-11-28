---
title: App Service Web-App in Linux Veelgestelde vragen over aaaAzure | Microsoft Docs
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
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="7eb63-104">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7eb63-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="7eb63-105">Hallo-versie van Web-App op Linux, momenteel niets over het toevoegen van functies en verbeteringen tooour platform maken.</span><span class="sxs-lookup"><span data-stu-id="7eb63-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="7eb63-106">Hier volgen enkele veelgestelde vragen (FAQ) die onze klanten is aangevraagd door ons via Hallo laatste maanden.</span><span class="sxs-lookup"><span data-stu-id="7eb63-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="7eb63-107">Als u een vraag, opmerking bij Hallo artikel hebt en we deze zo snel mogelijk moet beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="7eb63-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="7eb63-108">Ingebouwde afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="7eb63-108">Built-in images</span></span>

<span data-ttu-id="7eb63-109">**V:** ik wil toofork Hallo ingebouwde Docker-containers die Hallo platform biedt.</span><span class="sxs-lookup"><span data-stu-id="7eb63-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="7eb63-110">Waar vind ik die bestanden</span><span class="sxs-lookup"><span data-stu-id="7eb63-110">Where can I find those files?</span></span>

<span data-ttu-id="7eb63-111">**A:** vindt u alle Docker-bestanden op [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="7eb63-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="7eb63-112">U vindt alle Docker-containers op [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="7eb63-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="7eb63-113">**V:** wat Hallo verwachte waarden voor het starten van de sectie Hallo zijn bij het configureren van Hallo runtime stack?</span><span class="sxs-lookup"><span data-stu-id="7eb63-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="7eb63-114">**A:** voor Node.Js u Hallo PM2 configuratiebestand of opgeven het scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="7eb63-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="7eb63-115">Geef de naam van uw gecompileerde DLL voor .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7eb63-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="7eb63-116">Voor Ruby, kunt u Hallo Ruby script opgeven dat u wilt dat tooinitialize uw app.</span><span class="sxs-lookup"><span data-stu-id="7eb63-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="7eb63-117">Beheer</span><span class="sxs-lookup"><span data-stu-id="7eb63-117">Management</span></span>

<span data-ttu-id="7eb63-118">**V:** wat gebeurt er wanneer ik schakelaar Hallo opnieuw opstarten in hello Azure-portal?</span><span class="sxs-lookup"><span data-stu-id="7eb63-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="7eb63-119">**A:** dit is Hallo gelijkwaardige Docker opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7eb63-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="7eb63-120">**V:** kan ik Secure Shell (SSH) tooconnect toohello app container virtuele machine (VM) gebruiken?</span><span class="sxs-lookup"><span data-stu-id="7eb63-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="7eb63-121">**A:** Ja, kunt u doen via Hallo SCM-site, artikel selectievakje Hallo volgende voor meer informatie [SSH-ondersteuning voor Web-App op Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="7eb63-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="7eb63-122">**V:** wil toocreate een Linux-App Service-vlak via SDK of een ARM-sjabloon, hoe kan ik dit bereikt?</span><span class="sxs-lookup"><span data-stu-id="7eb63-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="7eb63-123">**A:** moet u tooset hello `reserved` veld van het Hallo-app service te`true`.</span><span class="sxs-lookup"><span data-stu-id="7eb63-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="7eb63-124">Continue integratie/implementatie</span><span class="sxs-lookup"><span data-stu-id="7eb63-124">Continuous integration/deployment</span></span>

<span data-ttu-id="7eb63-125">**V:** mijn web-app nog steeds de installatiekopie van een oude Docker-container wordt gebruikt nadat ik Hallo-installatiekopie op Docker-Hub hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7eb63-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="7eb63-126">Continue integratie/implementatie van aangepaste containers ondersteund?</span><span class="sxs-lookup"><span data-stu-id="7eb63-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="7eb63-127">**A:** tooset up continue integratie/implementatie voor installatiekopieën van het register van de Azure-Container of DockerHub door selectievakje Hallo volgende artikel [continue implementatie met de Azure-Web-App op Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="7eb63-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="7eb63-128">U kunt voor persoonlijke registers Hallo container vernieuwen te stoppen en vervolgens uw web-app te starten.</span><span class="sxs-lookup"><span data-stu-id="7eb63-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="7eb63-129">Of u kunt wijzigen of toevoegen van een dummy toepassingsinstelling tooforce een vernieuwing van de container.</span><span class="sxs-lookup"><span data-stu-id="7eb63-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="7eb63-130">**V:** ondersteunen testomgevingen?</span><span class="sxs-lookup"><span data-stu-id="7eb63-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="7eb63-131">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="7eb63-131">**A:** Yes.</span></span>

<span data-ttu-id="7eb63-132">**V:** kan ik gebruiken **webimplementatie** toodeploy mijn web-app?</span><span class="sxs-lookup"><span data-stu-id="7eb63-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="7eb63-133">**A:** Ja, moet u tooset een app instelling `WEBSITE_WEBDEPLOY_USE_SCM` te`false`.</span><span class="sxs-lookup"><span data-stu-id="7eb63-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="7eb63-134">Taalondersteuning</span><span class="sxs-lookup"><span data-stu-id="7eb63-134">Language support</span></span>

<span data-ttu-id="7eb63-135">**V:** bieden u ondersteuning voor niet-gecompileerde .NET Core apps?</span><span class="sxs-lookup"><span data-stu-id="7eb63-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="7eb63-136">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="7eb63-136">**A:** Yes.</span></span>

<span data-ttu-id="7eb63-137">**V:** u ondersteunen Composer als een afhankelijkheid manager voor PHP-apps?</span><span class="sxs-lookup"><span data-stu-id="7eb63-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="7eb63-138">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="7eb63-138">**A:** Yes.</span></span> <span data-ttu-id="7eb63-139">Tijdens een Git-implementatie moet Kudu detecteren die u een PHP-toepassing (met vriendelijke groet toohello aanwezigheid van een composer.json-bestand implementeert) en een installatie composer geactiveerd voor u.</span><span class="sxs-lookup"><span data-stu-id="7eb63-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="7eb63-140">Aangepaste containers</span><span class="sxs-lookup"><span data-stu-id="7eb63-140">Custom containers</span></span>

<span data-ttu-id="7eb63-141">**V:** ik mijn eigen aangepaste container gebruik.</span><span class="sxs-lookup"><span data-stu-id="7eb63-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="7eb63-142">Mijn app bevindt zich in Hallo `\home\` directory, maar ik kan mijn bestanden vinden wanneer ik Hallo inhoud bladeren met behulp van Hallo [SCM site](https://github.com/projectkudu/kudu) of een FTP-client.</span><span class="sxs-lookup"><span data-stu-id="7eb63-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="7eb63-143">Waar bevinden zich mijn bestanden?</span><span class="sxs-lookup"><span data-stu-id="7eb63-143">Where are my files?</span></span>

<span data-ttu-id="7eb63-144">**A:** We een SMB-share toohello koppelen `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="7eb63-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="7eb63-145">Hierdoor wordt de inhoud die is er overschreven.</span><span class="sxs-lookup"><span data-stu-id="7eb63-145">This will override any content that's there.</span></span>

<span data-ttu-id="7eb63-146">**V:** ik mijn eigen aangepaste container gebruik.</span><span class="sxs-lookup"><span data-stu-id="7eb63-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="7eb63-147">Ik wil niet Hallo platform toomount een SMB-share toohello `\home\`.</span><span class="sxs-lookup"><span data-stu-id="7eb63-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="7eb63-148">**A:** u kunt dit doen door de instelling Hallo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app instellen te`false`.</span><span class="sxs-lookup"><span data-stu-id="7eb63-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="7eb63-149">**V:** Mijn aangepaste container neemt een toostart lang en Hallo platform herstart Hallo container voordat deze is voltooid wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="7eb63-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="7eb63-150">**A:** kunt u Hallo lang Hallo platform wachten moet voordat u de container opnieuw configureren.</span><span class="sxs-lookup"><span data-stu-id="7eb63-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="7eb63-151">Dit kan worden gedaan door de instelling Hallo `WEBSITES_CONTAINER_START_TIME_LIMIT` app instelling toohello gewenste waarde in seconden.</span><span class="sxs-lookup"><span data-stu-id="7eb63-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="7eb63-152">Hallo standaardwaarde is 230 seconden en Hallo max is 600 seconden.</span><span class="sxs-lookup"><span data-stu-id="7eb63-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="7eb63-153">**V:** wat Hallo-indeling voor persoonlijke register server-url is?</span><span class="sxs-lookup"><span data-stu-id="7eb63-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="7eb63-154">**A:** u nodig hebt tooprovide Hallo volledige register url inclusief `http://` of `https://`.</span><span class="sxs-lookup"><span data-stu-id="7eb63-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="7eb63-155">**V:** wat Hallo-indeling voor Hallo installatiekopie met de naam in de optie persoonlijke register is?</span><span class="sxs-lookup"><span data-stu-id="7eb63-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="7eb63-156">**A:** moet u tooadd Hallo volledige installatiekopie met de naam waaronder Hallo persoonlijke register url (bv.</span><span class="sxs-lookup"><span data-stu-id="7eb63-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="7eb63-157">myacr.azurecr.IO/DotNet:Latest)</span><span class="sxs-lookup"><span data-stu-id="7eb63-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="7eb63-158">**V:** ik wil tooexpose meer dan één poort op de installatiekopie van mijn aangepaste container.</span><span class="sxs-lookup"><span data-stu-id="7eb63-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="7eb63-159">Is dit mogelijk?</span><span class="sxs-lookup"><span data-stu-id="7eb63-159">Is that possible?</span></span>

<span data-ttu-id="7eb63-160">**A:** momenteel, die niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7eb63-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="7eb63-161">**V:** kan ik mijn eigen opslag brengen?</span><span class="sxs-lookup"><span data-stu-id="7eb63-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="7eb63-162">**A:** momenteel die niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7eb63-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="7eb63-163">**V:** ik kan mijn aangepaste container bestand system of actief processen van Hallo SCM site niet doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="7eb63-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="7eb63-164">Waarom is dat?</span><span class="sxs-lookup"><span data-stu-id="7eb63-164">Why is that?</span></span>

<span data-ttu-id="7eb63-165">**A:** Hallo SCM site wordt uitgevoerd in een afzonderlijke container.</span><span class="sxs-lookup"><span data-stu-id="7eb63-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="7eb63-166">Hallo-bestandssysteem kan niet worden gecontroleerd of het uitvoeren van processen van Hallo app-container.</span><span class="sxs-lookup"><span data-stu-id="7eb63-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="7eb63-167">**V:** Mijn aangepaste container luistert tooa andere poort dan poort 80.</span><span class="sxs-lookup"><span data-stu-id="7eb63-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="7eb63-168">Hoe kan ik mijn app tooroute Hallo aanvragen toothat poort configureren?</span><span class="sxs-lookup"><span data-stu-id="7eb63-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="7eb63-169">**A:** hebben We automatische poortdetectie, ook kunt u een toepassing instelling opgeven **WEBSITES_PORT**, en geeft u het Hallo-waarde van het poortnummer Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="7eb63-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="7eb63-170">Eerder Hallo platform werd gebruikt `PORT` app instelt, we van plan bent toodeprecate Hallo Gebruik deze app instellen en verplaatsen toousing `WEBSITES_PORT` uitsluitend.</span><span class="sxs-lookup"><span data-stu-id="7eb63-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="7eb63-171">**V:** moet ik tooimplement HTTPS in Mijn aangepaste container.</span><span class="sxs-lookup"><span data-stu-id="7eb63-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="7eb63-172">**A:** Nee, Hallo platform HTTPS-beëindiging op Hallo gedeeld frontends verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7eb63-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="7eb63-173">Prijzen en SLA</span><span class="sxs-lookup"><span data-stu-id="7eb63-173">Pricing and SLA</span></span>

<span data-ttu-id="7eb63-174">**V:** wat wordt Hallo prijzen terwijl u de openbare preview Hallo?</span><span class="sxs-lookup"><span data-stu-id="7eb63-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="7eb63-175">**A:** u kosten in rekening gebracht half Hallo aantal uren dat uw app wordt uitgevoerd, met prijzen Hallo normale Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7eb63-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="7eb63-176">Dit betekent dat u een korting van 50 procent op normale prijzen van Azure App Service krijgt.</span><span class="sxs-lookup"><span data-stu-id="7eb63-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="7eb63-177">Overige</span><span class="sxs-lookup"><span data-stu-id="7eb63-177">Other</span></span>

<span data-ttu-id="7eb63-178">**V:** wat Hallo ondersteund tekens in namen van de instellingen van toepassing zijn?</span><span class="sxs-lookup"><span data-stu-id="7eb63-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="7eb63-179">**A:** u kunt alleen A-Z, a-z, 0-9 gebruiken en Hallo onderstrepingsteken voor toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="7eb63-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="7eb63-180">**V:** waar kan ik nieuwe functies aanvragen?</span><span class="sxs-lookup"><span data-stu-id="7eb63-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="7eb63-181">**A:** dient u uw idee op Hallo [forum met feedback van Web-Apps](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="7eb63-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="7eb63-182">'[Linux]' toohello titel van uw idee toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7eb63-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb63-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7eb63-183">Next steps</span></span>
* [<span data-ttu-id="7eb63-184">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="7eb63-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="7eb63-185">SSH-ondersteuning voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="7eb63-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="7eb63-186">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="7eb63-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="7eb63-187">Continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="7eb63-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
