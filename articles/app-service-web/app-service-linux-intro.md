---
title: aaaIntroduction tooAzure Web-App op Linux | Microsoft Docs
description: Meer informatie over Azure-Web-App op Linux.
keywords: Azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="5c7bb-104">Inleiding tooAzure Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="5c7bb-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5c7bb-105">Overview</span></span>
<span data-ttu-id="5c7bb-106">Klanten kunnen voor ondersteunde toepassing stacks Web-App gebruiken op Linux toohost web-apps systeemeigen op Linux.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="5c7bb-107">Hallo volgende sectie vindt u Hallo toepassing stacks die momenteel worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="5c7bb-108">Functies</span><span class="sxs-lookup"><span data-stu-id="5c7bb-108">Features</span></span>
<span data-ttu-id="5c7bb-109">Web-App op Linux ondersteunt momenteel Hallo toepassing stacks te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="5c7bb-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="5c7bb-110">Node.js</span></span>
    * <span data-ttu-id="5c7bb-111">4.4</span><span class="sxs-lookup"><span data-stu-id="5c7bb-111">4.4</span></span>
    * <span data-ttu-id="5c7bb-112">4.5</span><span class="sxs-lookup"><span data-stu-id="5c7bb-112">4.5</span></span>
    * <span data-ttu-id="5c7bb-113">6.2</span><span class="sxs-lookup"><span data-stu-id="5c7bb-113">6.2</span></span>
    * <span data-ttu-id="5c7bb-114">6.6</span><span class="sxs-lookup"><span data-stu-id="5c7bb-114">6.6</span></span>
    * <span data-ttu-id="5c7bb-115">6.9</span><span class="sxs-lookup"><span data-stu-id="5c7bb-115">6.9</span></span>
    * <span data-ttu-id="5c7bb-116">6.10</span><span class="sxs-lookup"><span data-stu-id="5c7bb-116">6.10</span></span>
    * <span data-ttu-id="5c7bb-117">6.11</span><span class="sxs-lookup"><span data-stu-id="5c7bb-117">6.11</span></span>
    * <span data-ttu-id="5c7bb-118">8.0</span><span class="sxs-lookup"><span data-stu-id="5c7bb-118">8.0</span></span>
    * <span data-ttu-id="5c7bb-119">8.1</span><span class="sxs-lookup"><span data-stu-id="5c7bb-119">8.1</span></span>
* <span data-ttu-id="5c7bb-120">PHP</span><span class="sxs-lookup"><span data-stu-id="5c7bb-120">PHP</span></span>
    * <span data-ttu-id="5c7bb-121">5.6</span><span class="sxs-lookup"><span data-stu-id="5c7bb-121">5.6</span></span>
    * <span data-ttu-id="5c7bb-122">7.0</span><span class="sxs-lookup"><span data-stu-id="5c7bb-122">7.0</span></span>
* <span data-ttu-id="5c7bb-123">.NET core</span><span class="sxs-lookup"><span data-stu-id="5c7bb-123">.Net Core</span></span>
    * <span data-ttu-id="5c7bb-124">1.0</span><span class="sxs-lookup"><span data-stu-id="5c7bb-124">1.0</span></span>
    * <span data-ttu-id="5c7bb-125">1.1</span><span class="sxs-lookup"><span data-stu-id="5c7bb-125">1.1</span></span>
* <span data-ttu-id="5c7bb-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="5c7bb-126">Ruby</span></span>
    * <span data-ttu-id="5c7bb-127">2.3</span><span class="sxs-lookup"><span data-stu-id="5c7bb-127">2.3</span></span>

<span data-ttu-id="5c7bb-128">Klanten kunnen hun toepassingen implementeren met behulp van:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="5c7bb-129">FTP</span><span class="sxs-lookup"><span data-stu-id="5c7bb-129">FTP</span></span>
* <span data-ttu-id="5c7bb-130">Lokale Git</span><span class="sxs-lookup"><span data-stu-id="5c7bb-130">Local Git</span></span>
* <span data-ttu-id="5c7bb-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="5c7bb-131">GitHub</span></span>
* <span data-ttu-id="5c7bb-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="5c7bb-132">Bitbucket</span></span>

<span data-ttu-id="5c7bb-133">Voor het schalen van toepassing:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-133">For application scaling:</span></span>

* <span data-ttu-id="5c7bb-134">Klanten kunnen worden geschaald web-apps omhoog en omlaag door het Hallo-laag van de App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="5c7bb-135">Klanten kunnen toepassingen uitbreiden en meerdere app-exemplaren binnen de grenzen Hallo van hun SKU uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5c7bb-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="5c7bb-136">Voor Kudu enkele van de basisfunctionaliteit Hallo:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="5c7bb-137">Omgevingen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-137">Environments</span></span>
* <span data-ttu-id="5c7bb-138">Implementaties</span><span class="sxs-lookup"><span data-stu-id="5c7bb-138">Deployments</span></span>
* <span data-ttu-id="5c7bb-139">Basic-console</span><span class="sxs-lookup"><span data-stu-id="5c7bb-139">Basic console</span></span>
* <span data-ttu-id="5c7bb-140">SSH</span><span class="sxs-lookup"><span data-stu-id="5c7bb-140">SSH</span></span>

<span data-ttu-id="5c7bb-141">Voor devops:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-141">For devops:</span></span>

* <span data-ttu-id="5c7bb-142">Faseringsomgevingen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-142">Staging environments</span></span>
* <span data-ttu-id="5c7bb-143">ACR en DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="5c7bb-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="5c7bb-144">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-144">Limitations</span></span>
<span data-ttu-id="5c7bb-145">Hello Azure-portal toont alleen functies die nu ook voor Web-App op Linux werken en verbergen Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="5c7bb-146">Als we het inschakelen van functies, zijn ze zichtbaar op Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="5c7bb-147">Sommige functies, zoals de integratie van virtueel netwerk, verificatie van Azure Active Directory/van derden of Kudu-site-uitbreidingen zijn nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="5c7bb-148">Zodra deze functies beschikbaar zijn, werken wij onze documentatie en blog over Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="5c7bb-149">Deze openbare preview is momenteel alleen beschikbaar in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c7bb-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="5c7bb-150">VS - west</span><span class="sxs-lookup"><span data-stu-id="5c7bb-150">West US</span></span>
* <span data-ttu-id="5c7bb-151">VS - oost</span><span class="sxs-lookup"><span data-stu-id="5c7bb-151">East US</span></span>
* <span data-ttu-id="5c7bb-152">West-Europa</span><span class="sxs-lookup"><span data-stu-id="5c7bb-152">West Europe</span></span>
* <span data-ttu-id="5c7bb-153">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="5c7bb-153">North Europe</span></span>
* <span data-ttu-id="5c7bb-154">Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="5c7bb-154">South Central US</span></span>
* <span data-ttu-id="5c7bb-155">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="5c7bb-155">North Central US</span></span>
* <span data-ttu-id="5c7bb-156">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="5c7bb-156">Southeast Asia</span></span>
* <span data-ttu-id="5c7bb-157">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="5c7bb-157">East Asia</span></span>
* <span data-ttu-id="5c7bb-158">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="5c7bb-158">Australia East</span></span>
* <span data-ttu-id="5c7bb-159">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="5c7bb-159">Japan East</span></span>
* <span data-ttu-id="5c7bb-160">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="5c7bb-160">Brazil South</span></span>
* <span data-ttu-id="5c7bb-161">Zuid-India</span><span class="sxs-lookup"><span data-stu-id="5c7bb-161">South India</span></span>

<span data-ttu-id="5c7bb-162">Web-Apps op Linux wordt alleen ondersteund in Hallo specifieke app-serviceabonnementen en heeft geen een Free of Shared-laag.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="5c7bb-163">App Service-abonnementen voor reguliere- en Linux-web-apps zijn ook sluiten elkaar wederzijds uit, zodat u een Linux-web-app in een niet-Linux-app service-abonnement maken kunt.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="5c7bb-164">Web-Apps op Linux moet worden gemaakt in een resourcegroep die geen niet-Linux web-apps in Hallo bevat dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5c7bb-165">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-165">Troubleshooting</span></span> ##

<span data-ttu-id="5c7bb-166">Wanneer uw toepassing toostart mislukt of als u wilt dat toocheck Hallo logboekregistratie van uw app, controleert u Hallo die docker Hallo logboekbestanden directory zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="5c7bb-167">U kunt toegang tot deze map via uw SCM-site of via de FTP.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="5c7bb-168">Hallo toolog `stdout` en `stderr` van de container, moet u tooenable **Docker-Container logboekregistratie** onder **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Logboekregistratie inschakelen][2]

![Met behulp van Kudu tooview Docker-Logboeken][1]

<span data-ttu-id="5c7bb-171">U toegang hebt tot Hallo SCM site uit **geavanceerde hulpmiddelen** in Hallo **ontwikkelingsprogramma's** menu.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c7bb-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-172">Next steps</span></span>
<span data-ttu-id="5c7bb-173">Zie Hallo volgen koppelingen tooget met op Linux-App Service is gestart.</span><span class="sxs-lookup"><span data-stu-id="5c7bb-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="5c7bb-174">U kunt vragen en problemen op boeken [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="5c7bb-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="5c7bb-175">Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="5c7bb-176">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="5c7bb-177">Met behulp van .NET Core in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="5c7bb-178">Met behulp van Ruby in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="5c7bb-179">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5c7bb-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="5c7bb-180">SSH-ondersteuning voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="5c7bb-181">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="5c7bb-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="5c7bb-182">Docker Hub continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="5c7bb-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png