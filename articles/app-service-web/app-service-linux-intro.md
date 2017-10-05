---
title: Inleiding tot Azure-Web-App op Linux | Microsoft Docs
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="64482-104">Inleiding tot Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="64482-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="64482-105">Overview</span></span>
<span data-ttu-id="64482-106">Klanten kunnen gebruiken Web-App op Linux op host WebApps systeemeigen op Linux voor stacks ondersteunde toepassing.</span><span class="sxs-lookup"><span data-stu-id="64482-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="64482-107">De volgende sectie geeft een lijst van de toepassing stapels die momenteel worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="64482-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="64482-108">Functies</span><span class="sxs-lookup"><span data-stu-id="64482-108">Features</span></span>
<span data-ttu-id="64482-109">Web-App op Linux ondersteunt momenteel de volgende toepassing stapels:</span><span class="sxs-lookup"><span data-stu-id="64482-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="64482-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="64482-110">Node.js</span></span>
    * <span data-ttu-id="64482-111">4.4</span><span class="sxs-lookup"><span data-stu-id="64482-111">4.4</span></span>
    * <span data-ttu-id="64482-112">4.5</span><span class="sxs-lookup"><span data-stu-id="64482-112">4.5</span></span>
    * <span data-ttu-id="64482-113">6.2</span><span class="sxs-lookup"><span data-stu-id="64482-113">6.2</span></span>
    * <span data-ttu-id="64482-114">6.6</span><span class="sxs-lookup"><span data-stu-id="64482-114">6.6</span></span>
    * <span data-ttu-id="64482-115">6.9</span><span class="sxs-lookup"><span data-stu-id="64482-115">6.9</span></span>
    * <span data-ttu-id="64482-116">6.10</span><span class="sxs-lookup"><span data-stu-id="64482-116">6.10</span></span>
    * <span data-ttu-id="64482-117">6.11</span><span class="sxs-lookup"><span data-stu-id="64482-117">6.11</span></span>
    * <span data-ttu-id="64482-118">8.0</span><span class="sxs-lookup"><span data-stu-id="64482-118">8.0</span></span>
    * <span data-ttu-id="64482-119">8.1</span><span class="sxs-lookup"><span data-stu-id="64482-119">8.1</span></span>
* <span data-ttu-id="64482-120">PHP</span><span class="sxs-lookup"><span data-stu-id="64482-120">PHP</span></span>
    * <span data-ttu-id="64482-121">5.6</span><span class="sxs-lookup"><span data-stu-id="64482-121">5.6</span></span>
    * <span data-ttu-id="64482-122">7.0</span><span class="sxs-lookup"><span data-stu-id="64482-122">7.0</span></span>
* <span data-ttu-id="64482-123">.NET core</span><span class="sxs-lookup"><span data-stu-id="64482-123">.Net Core</span></span>
    * <span data-ttu-id="64482-124">1.0</span><span class="sxs-lookup"><span data-stu-id="64482-124">1.0</span></span>
    * <span data-ttu-id="64482-125">1.1</span><span class="sxs-lookup"><span data-stu-id="64482-125">1.1</span></span>
* <span data-ttu-id="64482-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="64482-126">Ruby</span></span>
    * <span data-ttu-id="64482-127">2.3</span><span class="sxs-lookup"><span data-stu-id="64482-127">2.3</span></span>

<span data-ttu-id="64482-128">Klanten kunnen hun toepassingen implementeren met behulp van:</span><span class="sxs-lookup"><span data-stu-id="64482-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="64482-129">FTP</span><span class="sxs-lookup"><span data-stu-id="64482-129">FTP</span></span>
* <span data-ttu-id="64482-130">Lokale Git</span><span class="sxs-lookup"><span data-stu-id="64482-130">Local Git</span></span>
* <span data-ttu-id="64482-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="64482-131">GitHub</span></span>
* <span data-ttu-id="64482-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="64482-132">Bitbucket</span></span>

<span data-ttu-id="64482-133">Voor het schalen van toepassing:</span><span class="sxs-lookup"><span data-stu-id="64482-133">For application scaling:</span></span>

* <span data-ttu-id="64482-134">Klanten kunnen worden geschaald web-apps omhoog en omlaag door de laag van de App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="64482-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="64482-135">Klanten kunnen toepassingen uitbreiden en meerdere app-exemplaren binnen de grenzen van hun SKU uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64482-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="64482-136">Voor Kudu enkele van de basisfunctionaliteit:</span><span class="sxs-lookup"><span data-stu-id="64482-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="64482-137">Omgevingen</span><span class="sxs-lookup"><span data-stu-id="64482-137">Environments</span></span>
* <span data-ttu-id="64482-138">Implementaties</span><span class="sxs-lookup"><span data-stu-id="64482-138">Deployments</span></span>
* <span data-ttu-id="64482-139">Basic-console</span><span class="sxs-lookup"><span data-stu-id="64482-139">Basic console</span></span>
* <span data-ttu-id="64482-140">SSH</span><span class="sxs-lookup"><span data-stu-id="64482-140">SSH</span></span>

<span data-ttu-id="64482-141">Voor devops:</span><span class="sxs-lookup"><span data-stu-id="64482-141">For devops:</span></span>

* <span data-ttu-id="64482-142">Faseringsomgevingen</span><span class="sxs-lookup"><span data-stu-id="64482-142">Staging environments</span></span>
* <span data-ttu-id="64482-143">ACR en DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="64482-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="64482-144">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="64482-144">Limitations</span></span>
<span data-ttu-id="64482-145">De Azure portal toont alleen functies die nu ook voor Web-App op Linux werken en wordt de rest verborgen.</span><span class="sxs-lookup"><span data-stu-id="64482-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="64482-146">Als we het inschakelen van functies, zijn ze zichtbaar in de portal.</span><span class="sxs-lookup"><span data-stu-id="64482-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="64482-147">Sommige functies, zoals de integratie van virtueel netwerk, verificatie van Azure Active Directory/van derden of Kudu-site-uitbreidingen zijn nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="64482-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="64482-148">Zodra deze functies beschikbaar zijn, werken wij onze documentatie en blog over de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="64482-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="64482-149">Deze openbare preview is momenteel alleen beschikbaar in de volgende gebieden:</span><span class="sxs-lookup"><span data-stu-id="64482-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="64482-150">VS - west</span><span class="sxs-lookup"><span data-stu-id="64482-150">West US</span></span>
* <span data-ttu-id="64482-151">VS - oost</span><span class="sxs-lookup"><span data-stu-id="64482-151">East US</span></span>
* <span data-ttu-id="64482-152">West-Europa</span><span class="sxs-lookup"><span data-stu-id="64482-152">West Europe</span></span>
* <span data-ttu-id="64482-153">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="64482-153">North Europe</span></span>
* <span data-ttu-id="64482-154">Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="64482-154">South Central US</span></span>
* <span data-ttu-id="64482-155">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="64482-155">North Central US</span></span>
* <span data-ttu-id="64482-156">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="64482-156">Southeast Asia</span></span>
* <span data-ttu-id="64482-157">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="64482-157">East Asia</span></span>
* <span data-ttu-id="64482-158">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="64482-158">Australia East</span></span>
* <span data-ttu-id="64482-159">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="64482-159">Japan East</span></span>
* <span data-ttu-id="64482-160">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="64482-160">Brazil South</span></span>
* <span data-ttu-id="64482-161">Zuid-India</span><span class="sxs-lookup"><span data-stu-id="64482-161">South India</span></span>

<span data-ttu-id="64482-162">Web-Apps op Linux wordt alleen ondersteund in de specifieke app-serviceabonnementen en heeft geen een Free of Shared-laag.</span><span class="sxs-lookup"><span data-stu-id="64482-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="64482-163">App Service-abonnementen voor reguliere- en Linux-web-apps zijn ook sluiten elkaar wederzijds uit, zodat u een Linux-web-app in een niet-Linux-app service-abonnement maken kunt.</span><span class="sxs-lookup"><span data-stu-id="64482-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="64482-164">Web-Apps op Linux moet worden gemaakt in een resourcegroep die geen niet-Linux-web-apps in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="64482-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="64482-165">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="64482-165">Troubleshooting</span></span> ##

<span data-ttu-id="64482-166">Wanneer uw toepassing niet kan worden gestart of u wilt controleren van de logboekregistratie van uw app, Controleer u dat de Docker-Logboeken in de map met logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="64482-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="64482-167">U kunt toegang tot deze map via uw SCM-site of via de FTP.</span><span class="sxs-lookup"><span data-stu-id="64482-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="64482-168">Logboek de `stdout` en `stderr` van de container, moet u inschakelen **Docker-Container logboekregistratie** onder **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="64482-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Logboekregistratie inschakelen][2]

![Met behulp van Kudu Docker-logboeken weergeven][1]

<span data-ttu-id="64482-171">U toegang hebt tot de site SCM bij **geavanceerde hulpmiddelen** in de **ontwikkelingsprogramma's** menu.</span><span class="sxs-lookup"><span data-stu-id="64482-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64482-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64482-172">Next steps</span></span>
<span data-ttu-id="64482-173">Zie de volgende koppelingen aan de slag met App-Service op Linux.</span><span class="sxs-lookup"><span data-stu-id="64482-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="64482-174">U kunt vragen en problemen op boeken [ons forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="64482-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="64482-175">Het gebruik van een aangepaste Docker-afbeelding voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="64482-176">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="64482-177">Met behulp van .NET Core in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="64482-178">Met behulp van Ruby in Azure App Service-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="64482-179">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="64482-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="64482-180">SSH-ondersteuning voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="64482-181">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="64482-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="64482-182">Docker Hub continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="64482-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png